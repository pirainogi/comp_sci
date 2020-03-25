# Ruby
* (almost) everything is an object
  * numbers
  * strings
  * methods

* basic arithmetic
  * `1 + 1` => 2
  * `8 - 1` => 7
  * `10 * 2` => 20
  * `35 / 5` => 7
  * `2 ** 5` => 32
  * `5 % 3` => 2

* bitwise operators
  * `3 & 5` => 1
  * `3 | 5` => 7
  * `3 ^ 5` => 6

* arithmetic is just syntactic sugar for calling a method on an object
  * `1.+ (3)` => 4
  * `10.* 5` => 50
  * `100.methods.include?(:/)` => true

* special values are objects
  * `nil` => like `null` in other languages
    * `nil.class` => NilClass
  * `true`
    * `true.class` => TrueClass
  * `false`
    * `false.class` => FalseClass

* equality/inequality
  * `1 == 1 ` => true
  * `2 == 1 ` => false
  * `1 != 1` => false
  * `2 != 1` => true
  * `nil` is the only other falsy value except `false`
    * `!!nil` => false
    * `!!false` => faalse
    * `!!0` => true
    * `!!""` => true

* comparison operators
  * `1 < 10` => true
  * `1 > 10` => false
  * `2 <= 2` => true
  * `2 >= 2` => true
  * combined comparison operator returns `1` when the first argument is greater, `-1` when the second argument is greater, and `0` when they're equal
    * `1 <=> 10` => -1
    * `10 <=> 1` => 1
    * `1 <=> 1` => 0

* logical operators
  * `true && false` => false
  * `true || false` => true
  * alternative versions of the logical operators with lower precedence
    * intended for flow-control constructs to chain statements together until one returns true or false
    * `do_something() and do_something_else()`
      * `do_something_else` is only called if `do_something` succeeds
    * `do_something() or log_error()`
      * `log_error` only called if `do_something` fails

* String Interpolation
  * `placeholder = "use string interpolation"`
  * `"i can #{placeholder} when using double-quoted strings"`
  * combine strings using `+` but not with other types
    * `'hello' + 'world'` => "hello world"
    * `"hello" + 3` => TypeError: can't convert Fixnum into String
    * `"hello" + 3.to_s` => "hello 3"
    * `"hello" + #{3}` => "hello 3"
  * combine strings and operators
    * `"hello " * 3` => "hello hello hello "
  * append to a string
    * `"hello" << " world"` => "hello world"  

* print output with a newline at the end
  * `puts "I am printing!"` => "I am printing"
  * => nil
* print without a newline
  * `print "I am printing"` => "I am printing" => nil

* variables
  * `x = 25` => 25
  * `x` => 25
    * assignment returns the value assigned
    * can do multiple assigment
      * `x = y = 10` => 10
      * `x` => 10
      * `y` => 10
  * snake_case for variable names
  * use descriptive variable names
    * `path_to_project_root`
  * Symbols are immutable, reusable constants represented internally by an integer value. often used instead of strings to convey specific, meaningful values
    * `:pending.class` => Symbol
    * `status = :pending`
      * `status == :pending` => true
      * `status == "pending"` => false
      * `status == :approved` => false
  * strings can be converted into symbols and vice versa
    * `status.to_s` => "pending"
    * `"argon".to_sym` => :argon

* arrays
  * `array = [1, 2, 3, 4]`
  * can contain different types of items
    * `[1, "hello", false]` => [1, "hello", false]
  * arrays can be index from front and back
    * `array[0]` => 1
    * `array.first` => 1
    * `array[12]` => nil
    * `array[-1]` => 4
    * `array.last` => 4
  * or with a start index and length
    * `array[1, 2]` => [2, 3]
  * or with a range
    * `array[1..2]` => [2, 3]
  * arrays can be reversed and return a _new_ array with the reversed values
    * `array.reverse` => [4, 3, 2, 1]
    * `array.reverse!` => [4, 3, 2, 1]
      * with the bang, update the variable to represent the reversed array
  * [var] access is just syntactic sugar for calling a method `[]` on an object
    * `array.[] 0` => 1
    * `array.[] 12` => nil  
