<!-- -*- coding: utf-8; -*- -->

## Named_scope

La gema  *has\_finder*  ha sido incluida en Rails pero con un nombre diferente: **named\_scope**.

Para entender lo que significa este agregado en Rails vamos a ver los siguientes ejemplos:

        class Article < ActiveRecord::Base
          named_scope :published, :conditions => {:published => true}
          named_scope :containing_the_letter_a, :conditions => "body LIKE '%a%â€™"
        end

        Article.published.paginate(:page => 1)
        Article.published.containing_the_letter_a.count
        Article.containing_the_letter_a.find(:first)
        Article.containing_the_letter_a.find(:all, :conditions => {â€¦})

Instead of creating a new method named **published** to return all published posts, I'm using a **named\_scope** to do it for me. But it can go even further than this. Let's look at another example of how it can be used:

        named_scope :written_before, lambda { |time|
          { :conditions => ['written_on < ?', time] }
        }

        named_scope :anonymous_extension do
          def one
            1
          end
        end

        named_scope :named_extension, :extend => NamedExtension

        named_scope :multiple_extensions,
                :extend => [MultipleExtensionTwo, MultipleExtensionOne]

## Testing named\_scope with proxy\_options

**Named scopes** is a very interesting new feature for Rails 2.1, but after using it awhile you might have a hard time creating tests for more complex situations.

Let's look at an example:

                class Shirt < ActiveRecord::Base
                  named_scope :colored, lambda { |color|
                    { :conditions => { :color => color } }
                  }
                end

How to create a test that validates the generation of the scope ?

To solve this issue, the method **proxy\_options** was created. It allows us to examine the options used in **named_scope**. To test the code above we could write:

                class ShirtTest < Test::Unit
                  def test_colored_scope
                    red_scope = { :conditions => { :colored => 'red' } }
                    blue_scope = { :conditions => { :colored => 'blue' } }
                    assert_equal red_scope, Shirt.colored('red').scope_options
                    assert_equal blue_scope, Shirt.colored('blue').scope_options
                  end
                end
