# Basic Example

Require the library.

    require 'paramix'

Create a parametric mixin.

      module MyMixin
        include Paramix::Parametric

        parameterized do |params|

          public params[:name] do
            params[:value]
          end

        end
      end

Create a class that uses the mixin and set the parameter.

      class X
        include MyMixin[:name => 'f', :value=>1]
      end

Then the parameter is accessible.

      X.new.f.assert == 1


# Nested Parematric Mixins

If we create another parametric mixin which depends on the first.

    module AnotherMixin
      include Paramix::Parametric
      include MyMixin[:name => 'f', :value=>1]

      parameterized do |params|

        public params[:name] do
          params[:value]
        end

      end
    end

And a class for it.

    class Y
      include AnotherMixin[:name => 'g', :value=>2]
    end

We can see that the parameters stay with their respective mixins.

    Y.new.f.assert == 1
    Y.new.g.assert == 2

However if we do the same, but do not paramterize the first module then
the including module also become parametric.

    module ThirdMixin
      #include Paramix::Parametric
      include MyMixin

      parameterized do |params|

        public params[:name].succ do
          params[:value]
        end

      end
    end

And a class for it.

    class Z
      include ThirdMixin[:name => 'q', :value=>3]
    end

We can see that the value of the parameter has propogated up to its
ancestor parametric module.

    Z.new.q.assert == 3
    Z.new.r.assert == 3

