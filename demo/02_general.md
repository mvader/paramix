# Parametric Include

Load the library.

    require 'paramix'

Given a parametric mixin.

    module M
      include Paramix::Parametric

      parameterized do |params|

        public :f do
          params[:p]
        end

      end
    end

We can inlcude the parameteric module in a some classes.

    class I1
      include M[:p => "mosh"]
    end

    class I2
      include M[:p => "many"]
    end

And the result will vary according to the parameter set.

    I1.new.f  #=> "mosh"
    I2.new.f  #=> "many"


# Parametric Extension

We can also extend classes witht the mixin.

    class E1
      extend M[:p => "mosh2"]
    end

    class E2
      extend M[:p => "many2"]
    end

And the results will likewise work as expected.

     E1.f  #=> "mosh2"
     E2.f  #=> "many2"


# Dynamically Defined Methods

Parametric mixins can be used to define dynamic code.

    module N
      include Paramix::Parametric

      parameterized do |params|
        attr_accessor params[:a]
      end
    end

Now if we include this module we will have new attributes based on
the parameter assigned.

    class D1
      include N[:a => "m1"]
    end

    class D2
      include N[:a => "m2"]
    end

    d1 = D1.new
    d1.m1 = :yes1

    d1.m1  #=> :yes1

    d2 = D2.new
    d2.m2 = :yes2

    d2.m2  #=> :yes2

