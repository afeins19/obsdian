say you have a knapsack. Given a set of items, each with a weight and a value, determine which items to include in the collection so that the total weight is less than or equal to a given limit and the total value is as large as possible. Note that we may subdivide items into arbitratily small quantities 
### Applications of this Problem
- find the least wasteful way to cut raw materials
- selection of investments and portfolios 
- selection of assets for asset-backed securitization 

### Example 

| A           | 1   | 2   | 3    | 4    | 5   | 6   | 7   |
| ----------- | --- | --- | ---- | ---- | --- | --- | --- |
| Cost ($)    | 10  | 6   | 14   | 6    | 9   | 20  | 4   |
| Weight (kg) | 2   | 3   | 6    | 8    | 1   | 5   | 8   |
| $/kg        | 5   | 2   | 2.33 | 0.75 | 9   | 4   | 0.5 |

### Amount of each item to take 
| A           | 1   | 2   | 3    | 4    | 5   | 6   | 7   |
| ----------- | --- | --- | ---- | ---- | --- | --- | --- |
| Cost ($)    | 10  | 6   | 14   | 6    | 9   | 20  | 4   |
| Weight (kg) | 2   | 3   | 6    | 8    | 1   | 5   | 8   |
| $/kg        | 5   | 2   | 2.33 | 0.75 | 9   | 4   | 0.5 |
| Include     | 1   | 2   | 5    | 6    | 1   | 0   | 0   |
$$\sum{item}\times{price} = 1 * 1 + 1 * 2 + 5 + 6 + \frac{1}{3} = 15$$
