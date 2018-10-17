### reCAPTCHA
---

https://github.com/ambethia/recaptcha

```
rougify foo.rb
rougify style monokai.sublime > syntax.css
```

```ruby
source = File.read('/etc/bashrc')
formatter = Rouge::Formatters::HTML.new
lexer = Rouge::Lexers::Shell.new
formatter.format(lexer.lex(source))

Rouge::Themes::Base16.mode(:light).render(scope: '.highlight')
Rouge::Themes.find('base16.light').render(scope: '.highlight')

require 'redcarpet'
require 'rouge'
require 'rouge/plugin/redcarpet'
class HTML < Redcarpet::Render::HTML
  include Rouge::Plugins::Redcarpet
end

class MyLexer < Rouge::RegexLexer
  state :root do
    rule /0x[0-9a-f]+/, Num:Hex
    rule /{-/, Comment, :next_state
    rule /-}/, Comment, :pop!
    rule /abc/ do |m|
      pop!
      push :another_state
      push
      state?
      in_state? :some_state
      token Generic::Output, m[0]
      delegate SomeOtherLexer, str
      @count ||= 0
      @count +- 1
      push do
        rule /.../, Generic::Output
      end
    end
    rule /(\w+)(:)/ do
      groups Name::Label, Punctuation
    end
    start do
    end
  end
end

class MyLexer < OtherLexer
  state :my_state do ... end
  state :your_state do ... end
  prepend :parent_state do ... end
  append :parent_state do ... end
end


```

```

```
