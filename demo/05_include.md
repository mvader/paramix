# Include

Given include with parametric mixins.

    module MI
      include Paramix::Parametric

      parameterized do |params|

        public :f do
          params[:p]
        end

      end
    end

    class I1
      include MI[:p => "mosh"]
    end

    class I2
      include MI[:p => "many"]
    end

Then it should vary the return value of the instance methods.

    I1.new.f.should == "mosh"
    I2.new.f.should == "many"

