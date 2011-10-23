# Paramix

| Project    | Paramix                             |
|:-----------|:------------------------------------|
| Copyright  | (c) 2006 Rubyworks                  |
| License    | BSD-2-Clause                        |
| Website    | http://rubyworks.github.com/paramix |
| GitHub     | http://github.com/rubyworks/paramix |
| Status     | [![Build Status](https://secure.travis-ci.org/rubyworks/paramix.png)](http://travis-ci.org/rubyworks/paramix) |

## Description

Parametric Mixins provides an easy means to "functionalize" modules.
The module can then be differentiated upon usage according to the
parameters provided.


## Release Notes

Please see the HISTORY.rdoc file.


## Example

Here is a simple example that uses a a parameter 
to define a method and another parameter to define
it's return value.

    module M
      include Paramix::Parametric

      paramaterized do |params|
        define_method params[:name] do
          params[:value]
        end
      end
    end

    class X
      include M[:name=>'foo', :value='bar']
    end

    X.new.foo  #=> 'bar'


## Copyrights

Copyright (c) 2006 Thomas Sawyer

This program is ditributed unser the terms of the BSD-2-Clause license.

See COPYING.rdoc file for details.

