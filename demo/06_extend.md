# Extend

Given extend with parametric mixins.

    module ME
      include Paramix::Parametric

      parameterized do |params|

        public :f do
          params[:p]
        end

      end
    end

    class E1
      extend ME[:p => "mosh"]
    end

    class E2
      extend ME[:p => "many"]
    end

Then should vary the return value of the class methods.

    E1.f.should == "mosh"
    E2.f.should == "many"

