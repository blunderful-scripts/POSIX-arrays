# Examples of translation from Bash syntax to POSIX-arrays syntax

## Indexed arrays

### Declaring an array, assigning and adding values, unsetting elements

Bash: `declare test_arr=(a b c)`

POSIX-arrays:`declare_i_arr test_arr a b c`

##

Bash: `test_arr[100]="this is a test"`

POSIX-arrays:`set_i_arr_el test_arr 100 "this is a test"`

##

Bash: `test_arr+=("this is another test")`

POSIX-arrays:`add_i_arr_el test_arr "this is another test"`

### Getting values and indices
Bash: `echo "value for index 100 is $test_arr[100]"`

POSIX-arrays: `get_i_arr_val test_arr 100 value; echo "value for index 100 is $value"`

##

Bash: `echo "all values of test_arr are '${test_arr[*]}'"`

POSIX-arrays: `get_i_arr_values test_arr values; echo "all values of test_arr are '$values'"`

POSIX-arrays (to get a sorted list): `get_i_arr_values -s test_arr values; echo "sorted values of test_arr are '$values'"`

##

Bash: `echo "all indices of test_arr are '${!test_arr[*]}'"`

POSIX-arrays: `get_i_arr_indices test_arr indices; echo "all indices of test_arr are '$indices'"`

POSIX-arrays (to get a sorted list): `get_i_arr_indices -s test_arr indices; echo "sorted indices of test_arr are '$indices'"`

##

Bash: `echo "test_arr has '${#test_arr[@]}' elements"`

POSIX-arrays: `get_i_arr_el_cnt test_arr el_cnt; echo "test_arr has '$el_cnt' elements"`

##

Bash: `indices=( "${!test_arr[@]}" ); echo "max index of test_arr is '${indices[-1]}'"`

POSIX-arrays: `get_i_arr_max_index test_arr maxindex; echo "max index of test_arr is '$maxindex'"`

##

Bash: `echo "last value of test_arr is '${test_arr$[-1]}'"`

POSIX-arrays: `get_i_arr_last_val test_arr lastval; echo "last value of test_arr is '$lastval'"`

##

### Unsetting arrays
Bash: `declare temp_arr=("this array will be destroyed"); unset temp_arr`

POSIX-arrays: `declare_i_arr temp_arr "this array will be destroyed"; unset_i_arr temp_arr`

### Working with loops
Bash:
```
declare test_arr=("no_whitespaces_value1" "no_whitespaces_value2")
for value in ${test_arr[@]}; do
    echo "$value"
done
```
POSIX-arrays:
```
declare_i_arr test_arr "no_whitespaces_value1" "no_whitespaces_value2"
get_i_arr_values test_arr values
for value in $values; do
    echo "$value"
done
```

##

Bash:
```
declare test_arr=("i_don't_have_whitespaces" "i have whitespaces")
for value in ${test_arr[@]}; do
    echo "$value"
done
```
POSIX-arrays (here we need to loop over indices rather than over values, to avoid whitespace issues):
```
declare_i_arr test_arr "i_don't_have_whitespaces" "i have whitespaces"
get_i_arr_indices test_arr indices
for index in $indices; do
    get_i_arr_val "$index" value
    echo "$value"
done
```

##

Bash:
```
for index in ${!test_arr[@]}; do
    echo "$index"
done
```
POSIX-arrays:
```
get_i_arr_indices test_arr indices
for index in $indices; do
    echo "$index"
done
```


## Associative arrays

### Declaring an array, assigning and adding values, unsetting elements

Bash: `declare -A test_arr=([key1]=val1 [key2]=val2)`

POSIX-arrays: `declare-a-arr test_arr key1=val1 key2=val2`

##

Bash: `test_arr[key]="test value"`

POSIX-arrays: `set_a_arr_el test_arr key="test value"`

##

Bash: `unset test_arr[key]`

POSIX-arrays: `unset_a_arr_el test_arr key`
##

### Getting values, keys and parameters

Bash: `echo "value for 'key': '${test_arr[key]}'"`

POSIX-arrays: `get_a_arr_val test_arr value; echo "value for 'key': '$value'"`

##

Bash: `echo "all values of test_arr are '${test_arr[*]}'"`

POSIX-arrays: `get_a_arr_values test_arr values; echo "all values of test_arr are '$values'"`

POSIX-arrays (to get a sorted by key list): `get_a_arr_values -s test_arr values; echo "sorted by key values of test_arr are '$values'"`

##

Bash: `echo "all keys of test_arr are '${!test_arr[*]}'"`

POSIX-arrays: `get_a_arr_keys test_arr keys; echo "all keys of test_arr are '$keys'"`

POSIX-arrays (to get a sorted list): `get_a_arr_keys -s test_arr keys; echo "sorted keys of test_arr are '$keys'"`

##

Bash: `echo "test_arr has '${#test_arr[@]}' elements"`

POSIX-arrays: `get_a_arr_el_cnt test_arr el_cnt; echo "test_arr has '$el_cnt' elements"`

### Unsetting arrays
Bash: `unset temp_arr`

POSIX-arrays: `unset_i_arr temp_arr`

### Working with loops

Bash:
```
for value in ${test_arr[@]}; do
    echo "$value"
done
```
POSIX-arrays:
```
get_a_arr_values test_arr values
for value in $values; do
    echo "$value"
done
```
##

Bash:
```
for key in ${!test_arr[@]}; do
    echo "$key"
done
```
POSIX-arrays:
```
get_a_arr_keys test_arr keys
for key in $keys; do
    echo "$key"
done
```
