# Bash Helper Snippets

#### Check if file exists

```bash
if [ ! -f /tmp/foo.txt ]; then
    echo "File not found!"
fi
```

#### Manipulate CSV file

{% code title="csv\_split.sh" %}
```bash
# Manipulate csv data using bash
#
# You can use read to split the CSV, then output the desired number of
# columns.

cat test.csv | while read line; do
  IFS=\; read -ra COL <<< "$line"
  echo "${COL[0]};${COL[1]};${COL[2]};${COL[3]};${COL[4]};"
done

# For example, with test.csv containing:

1;2;3;4
1;2;3;4;5
1;2;3;4;
1;2;3;4;5;

# The above script outputs:

1;2;3;4;;
1;2;3;4;5;
1;2;3;4;;
1;2;3;4;5;
```
{% endcode %}



