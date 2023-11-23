# POSIX-arrays
POSIX-compatible shell functions emulating some aspects of arrays

## Usage
**Indexed arrays**:

`declare_i_arr <array_name> [value] [value] ... [value]` - resets the array and assigns values to sequential indexes, starting from 1

`set_i_arr_el <array_name> <index> [value]` - assigns [value] to <index>. Indexes should always be positive integer numbers. This acts as a sparse array, so indexes don't have to be sequential.

`get_i_arr_el <array_name> <index>`

**Examples**:

Input:

```
set_i_arr_el test_arr 10 some_val
get_i_arr_el test_arr 10
```

Output: `some_val`

Input:

```
declare_i_arr test_arr val1 val2 "val 123 etc"
get_i_arr_el test_arr 3
```

Output: `val3 123 etc`

**Associative arrays**:

`set_a_arr_el <array_name> <key>=[value]`

`get_a_arr_el <array_name> <key>`

**Example**:

Input:

```
set_a_arr_el test_arr some_key="this is a test"
get_a_arr_el test_arr some_key
```

Output: `this is a test`

## More details
- The emulated arrays are stored in dynamically created variables. The base for is the same as the emulated array's name, except when creating the variable, the function prefixes its name with `emu_[x]_`.
- For example, if calling a function to create an indexed array: `set_i_arr_el test_arr 5 "test_value"`, the function will create a variable called 'emu_i_test_arr' and store the value in it.
- If calling a function to create an associative array: `set_a_ar_el test_arr test_key=test_val`, the function will create a variable called 'emu_a_test_arr' and store the key=value pair in it.
- The delimiter used internally is '#'. Which means this specific symbol should not be a part of any strings passed to the function. If for some reason you need arrays that can hold this symbol, change the code to use another delimiter.
- Functions check for correct number of arguments and return an error if it's incorrect.
- The indexed array functions check the key to make sure it's a positive integer, and return an error otherwise.
- As is default for shells, if you try request a value for an index or for a key that has not been set previously, the functions will output an empty string and not return an error.
- The indexed array effectively works as a sparse array, meaning that the indexes do not have to be continuous and sequential. For example, you can set a value for index 10 and for index 100 while all other indexes will not be set.
- The declare function for the indexed array is not necessary to create an array. It's just a way to set N values sequentially in one command. Otherwise you can create an array by simply calling the set_[x]_arr_el() function.
