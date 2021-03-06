# Nested Parametric Mixins

Given nested modules where inner most module is parametric.

    m = Module.new do
      include Paramix::Parametric

      parameterized do |params|
        public :f do
          params[:p]
        end
      end
    end

    n = Module.new do
      include m[:p=>"NMp"]
    end

    i = Class.new do
      include n
    end

    e = Class.new do
      extend  n
    end

Then

    i.new.f.should == "NMp"

And

    e.f.should == "NMp"

Nested parametric mixins with parameters.

    m = Module.new do
      include Paramix::Parametric

      parameterized do |params|
        public :f do
          params[:p]
        end
      end
    end

    n = Module.new do
      include Paramix::Parametric
      include m[:p=>"NMp"]

      parameterized do |params|
        public :g do
          params[:p]
        end
      end
    end

    i = Class.new do
      include n[:p => "INp"]
    end

    e = Class.new do
      extend n[:p => "ENp"]
    end

Then

      i.new.f.should == "NMp"

And

      i.new.g.should == "INp"

And

      e.f.should == "NMp"

And
     
     e.g.should == "ENp"

Given nested parametric mixins without parameters.

    m = Module.new do
      include Paramix::Parametric

      parameterized do |params|
        public :f do
          params[:p]
        end
      end
    end

    n = Module.new do
      include m

      parameterized do |params|
        public :g do
          params[:p]
        end
      end
    end

    i = Class.new do
      include n[:p => "INp"]
    end

    e = Class.new do
      extend n[:p => "ENp"]
    end

Then

    i.new.f.should == "INp"

And

    i.new.g.should == "INp"

And

    e.f.should == "ENp"

And

    e.g.should == "ENp"

Given nested parametric mixins where the outer is not parameterized.

    m = Module.new do
      include Paramix::Parametric

      parameterized do |params|
        public :f do
          params[:p]
        end
      end
    end

    n = Module.new do
      include Paramix::Parametric
      include m[:p=>"NMp"]
    end

    i = Class.new do ; include n[] ; end
    e = Class.new do ; extend  n[] ; end

    ix = Class.new do ; include n[:p=>"IxNp"] ; end
    ex = Class.new do ; extend  n[:p=>"ExNp"] ; end

Then

    i.new.f.should == "NMp"


And

    e.f.should == "NMp"

And

    i.new.f.should == "NMp"

And

    e.f.should == "NMp"


Given nested parametric mixins both parameterized.

    m = Module.new do
      include Paramix::Parametric

      parameterized do |params|
        public :f do
          params[:p]
        end
      end
    end

    n = Module.new do
      include Paramix::Parametric
      include m[:p=>"mood"]

      parameterized do |params|
        public :g do
          params[:p]
        end
      end
    end

    i = Class.new do
      include n[]
    end

    e = Class.new do
      extend n[]
    end

Then

    i.new.f.should == "mood"

And

    i.new.g.should == nil  # TODO: or error ?

And

    e.f.should == "mood"

And

    e.g.should == nil

