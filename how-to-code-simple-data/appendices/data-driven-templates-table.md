To use the following table:
Start with the data type of the information you've chosen to represent in the program. Select the row that matches that type.

| Type of data | cond question (if applicable) | Body or cond answer (if applicable) |
|:--------------:|:-------------------------------:|:-------------------------------------:|
| **Atomic non-distinct**<br /><br /><br />`Number`<br /><br /><br />`String`<br /><br /><br />`Boolean`<br /><br /><br />`Image`<br /><br /><br />`Interval`<br /><br /><br />etc. | **Appropriate predicate**<br /><br /><br />`(number? x)`<br /><br /><br />`(string? x)`<br /><br /><br />`(boolean? x)`<br /><br /><br />`(image? x)`<br /><br /><br />`(and (<= 0 x) (< x 10))`<br /><br />etc. | `(... x)` |
| **Atomic Distinct**<br /><br /><br />`"red"`<br /><br /><br />`#false`<br /><br /><br />`empty`<br /><br /><br />etc. | **Appropriate predicate**<br /><br />`(string=? x "red")`<br /><br /><br />`(false? x)`<br /><br /><br />`(empty? x)`<br /><br /><br />etc. | `(...)`
| **One of**<br /><br /><br />Enumerations<br /><br /><br />Itemizations | | cond with one class per subclass of one-of, where each question and answer expression is formed by following the rule in the question or answer column of this table for the corresponding case.<br /><br />You can use else for itemizations and large enumerations, but they should not be used for regular enumerations. |
| **Compound**<br /><br /><br />`Position`<br /><br /><br />`Firework`<br /><br /><br />`Ball`<br /><br /><br />cons<br /><br /><br />etc.<br /><br /><br /><br /><br /> | **Predicate from structure**<br /><br />`(posn? x)`<br /><br /><br />`(firework? x)`<br /><br /><br />`(ball? x)`<br /><br /><br />`(cons? x)` (often `else`)<br /><br />etc.<br /><br /><br /><br /><br /> | **All selectors**<br /><br /><br />`(... (posn-x x) (posn-y x))`<br /><br /><br />`(... (firework-y x) (firework-color x))`<br /><br /><br />`(... (ball-x x) (ball-dx x))`<br /><br /><br />`(... (first x) (rest x))`<br /><br /><br />etc.<br /><br /><br />Then consider the result type of each selector call and wrap the accessor expression using the table with that type. |
| **Other non-primitive type reference**<br /><br /><br /><br /><br /> | **Predicate, usually from structure definition**<br /><br />`(firework? x)`<br /><br />`(person? x)` | **Call to other type's template function**<br /><br /><br />`(fn-for-firework x)`<br /><br />`(fn-for-person x)` |
| **Self reference**<br /><br /><br /><br /> | | **Form natural recursion with a call to this type's template function**<br /><br />`(fn-for-los (rest los))` |
| **Mutual reference**<br /><br /><br /><br /><br /> | | **Call to other type's template function**<br /><br />`(fn-for-lod (dir-subdirs d))`<br /><br />`(fn-for-dir (first lod))` |