# Derive gender from a column of first names

*This tutorial is based on ["From OMBD to Gender Data on Film Directors."](http://blog.silk.co/post/127234807482/from-ombd-to-gender-data-on-film-directors-how-to)*

What can you do if you want to perform a gender-based analysis of your dataset, but "gender" isn't a category in your data? You can use computational methods to perform an educated guess, based on the first name of the person.

Is it flawless? No way. First names can often be ambiguous, and a woman could easily have a "man's" name, or vice versa. But often a name is all we have, and sometimes the benefits of performing a gender-based analysis outweigh the problems of computationally deriving gender.

In this tutorial, we'll use a tool called genderize.io. Genderize takes advantage of a database of thousands of names and genders to give you a probable gender for a name. It also gives you a probability for each guess at gender. You can read more about it [here](https://genderize.io/).

An important caveat: Genderize will only give you 1,000 guesses at gender per day, so you may have to divide up your names among team members, or use Genderize in installments.

## Make sure you have a column that contains only first names.

If your column contains first and last names, you'll have to use OpenRefines split cells function to isolate first names in their own column.

![][1]

[1]: images/derive-gender-from-a-column-of-first-names/make-sure-you-have-a-column-that-contains-only-first-names.png

## Load your spreadsheet into Google Drive

Open your CSV in Google Sheets.

![][2]

[2]: images/derive-gender-from-a-column-of-first-names/load-your-spreadsheet-into-google-drive.png

## Insert five blank columns to the right of the column of first names

You'll need those columns to store the information from Genderize.

![][3]

[3]: images/derive-gender-from-a-column-of-first-names/insert-five-blank-columns-to-the-right-of-the-column-of-first-names.png

## Enter the formula to query Genderize

In the column to the right of you column of first names, enter the following formula:

     ="https://api.genderize.io/?name="&lower(A2)

Except instead of **A2**, enter the letter and number that corresponds to the cell containing the first name in your first-name column.

![][4]

[4]: images/derive-gender-from-a-column-of-first-names/enter-the-formula-to-query-genderize.png

## Copy that formula into every cell in that column

You can do that by grabbing the tiny blue square at the bottom right of the cell and dragging it all the way to the bottom of the column. Excel will automatically modify the cell reference (like A2) so that it corresponds to the cell in the appropriate row.

![][5]

[5]: images/derive-gender-from-a-column-of-first-names/copy-that-formula-into-every-cell-in-that-column.png

## Enter the formula to send your query to Genderize

That formula looks like this:

     =IMPORTDATA(B2)

except instead of B2, reference the cell in your own spreadsheet that refers to the formula you added in the last step.

Now drag that formula all the way down to the end of the column, just the way you did in the previous step. 

As you drag, the contents of the cell will read "Loading..." indicating that Genderize is querying its database.

![][6]

[6]: images/derive-gender-from-a-column-of-first-names/enter-the-formula-to-send-your-query-to-genderize.png

## You have gender!

In the blank columns you added earlier, Genderize will fill in the following information: gender, the degree of certainty of that gender (from 0 to 1), and the number of data entries it examined to arrive at the response.

You may not need the probability and count information, but it's good to know.

![][7]

[7]: images/derive-gender-from-a-column-of-first-names/you-have-gender-.png

## Copy the gender column and paste it as a value (1)

You'll probably want to modify the cells that being **gender:"** so that they simply read **male**, **female**, and **null**. But right now, if you try to modify them, Google Sheets will get confused, because it just wants to display the results of its query to Genderize.

To get around this, first insert a new column after the column that contains the **count** information.

![][8]

[8]: images/derive-gender-from-a-column-of-first-names/copy-the-gender-column-and-paste-it-as-a-value--1-.png

## Copy the gender column and paste it as a value (2)

Now copy the entire column that contains gender information.

![][9]

[9]: images/derive-gender-from-a-column-of-first-names/copy-the-gender-column-and-paste-it-as-a-value--2-.png

## Copy the gender column and paste it as a value (3)

Finally, place your cursor in the first cell of your new, blank column. From the **Edit** menu, choose **Paste special** and then choose **Values only**. 

This will paste only the contents of your gender cells, without any of the formulas used to calculate those values.

![][10]

[10]: images/derive-gender-from-a-column-of-first-names/copy-the-gender-column-and-paste-it-as-a-value--3-.png

## Get rid of the extra characters

The easiest way is to use **Find and replace** to first replace **gender:** with nothing and then replace **" **with nothing.

![][11]

[11]: images/derive-gender-from-a-column-of-first-names/get-rid-of-the-extra-characters.png

## You have a column of just gender!

Not too hard! You can get rid of the extra columns (columns **B** through **F** in the spreadsheet below) if you want.

![][12]

[12]: images/derive-gender-from-a-column-of-first-names/you-have-a-column-of-just-gender-.png
