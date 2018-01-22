# 2018-01-08

## Stack matrices from different sheets into a single sheet

In this data set, a course can be rated on 69 different criteria. There are 12 multiple courses, each rated by 9 evaluators on all 69 criteria. To enter the data, each evaluator received a separate sheet containing a 69 x 12 matrix with criteria in rows and courses in columns. After entering the data, the evaluators needed to gather all their responses in a single sheet, stacked vertically. They also wanted a new column to indicate which evaluator is responsible for a given row of ratings. 

- Source data located in sheets `qVE`, `qSG`, etc.
    - columns A thru N contain the rating for a given class on each sheet
    - first row of each column contains name of the class
- Formula entered into A2 of destination sheet
    - The structure `{ ; }` stacks arrays vertically
    - The structure `{ , }` stacks arrays horizontally
    - The `transpose(split(rept()))` pattern creates a vertical, single-column array of 69 cells, each containing the same string
- Result is that responses are stacked from multiple sheets, with a sheet-specific identifier copied into a final column for all cells corresponding to that sheet.


```javascript
= {
  { qVE!A2:N, transpose(split(rept("VE"&",",69),",")) };
  { qSG!A2:N, transpose(split(rept("SG"&",",69),",")) };
  { qSH!A2:N, transpose(split(rept("SH"&",",69),",")) };
  { qYG!A2:N, transpose(split(rept("YG"&",",69),",")) };
  { qJH!A2:N, transpose(split(rept("JH"&",",69),",")) };
  { qMH!A2:N, transpose(split(rept("MH"&",",69),",")) };
  { qJK!A2:N, transpose(split(rept("JK"&",",69),",")) };
  { qKR!A2:N, transpose(split(rept("KR"&",",69),",")) };
  { qMR!A2:N, transpose(split(rept("MR"&",",69),",")) }
}
```
