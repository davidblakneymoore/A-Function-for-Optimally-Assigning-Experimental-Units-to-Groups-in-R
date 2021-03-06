# A Function for Optimally Assigning Experimental Units to Groups in R

To assign experimental units to treatments, it might be worthwhile to ensure that means or standard deviations of a variable or of some variables that define experimental units are as equal as possible between treatment groups. This function takes measurements from potential experimental units and assigns treatment groups that equalize means and standard deviations as much as possible.

Furthermore, if you have more potential experimental units than you need for your project, this function will optimally determine which experimental units best equalize means and standard deviations based on the number of treatment groups you'll have and the number of experimental units you'll have in each group.

This function can take more than one measurement variable into account to determine the optimal combination. It can also handle both numeric and categorical variables. Categorical variables are converted into dummy variables to ensure that categories are split up equally across groups, and weights associated with each categorical variable are divide by the number of groups to ensure that categorical variables are not weighted more heavily than they were intended to be.

Before splitting items up into groups, this function first rescales each measurement variable to a standard normal distribution by subtracting the column mean from each measurement and then by dividing each measurement by the column standard deviation. By rescaling the measurements, it's possible to compare mean and standard deviation variability between groups between measurements later on.

This function optionally uses the `comboGroups()` function from the `RcppAlgos` package.

This function takes 10 arguments. The first, second, fourth, and fifth arguments are required.

`Identifiers` is a vector containing the names of the potential experimental units.

`...` is a vector, or are vectors, containing the  measurements that will be used to optimally assign groups. Although this argument will typically contain numeric data, this argument could contain one or more characer or factor vector or vectors. Dummy variables will be created for categorical variables so that these categories can be optimally split up between groups as well.

`Data_Frame` is an optional data frame to include such that column names can be supplied for the `Identifiers` and the `...` arguments. The data frame that these columns are from should be provided for this `Data_Frame` argument.

`Number_of_Groups` is the number of treatment groups you wish to have.

`Number_of_Items_in_Each_Group` is the number of experimental units you wish to have in each treatment group. This function assumes that each treatment group contains the same number of experimental units.

`Variable_Weights = rep(1, ncol(cbind(...)))` are the weights given to each of the provided variables in the function. The default value, `rep(1, ncol(cbind(...)))`, ensures that each variable is weighed equally.

`Mean_Weight = 1` is the weight given to the mean for each variable. If it is preferable that means are less variable than standard deviations, you may opt to make the value of this argument greater than the value of the subsequent argument. The default value, `1`, assigns a weight of 1 to means.

`Standard_Deviation_Weight = 1` is the weight given to the standard deviation for each variable. If it is only necessary to consider and minimize the variability in group means - if variability in standard deviations can be ignored - you may opt to assign the value of 0 to this argument. The default value, `1`, assigns a weight of 1 to standard deviations.

`Number_of_Combinations_to_Report` is the number of combinations reported. Combinations are reported in order starting with the combination that has the least variabillity in means and standard deviations.

`Use_the_RcppAlgos_Package = TRUE` takes a logical value and signifies whether or not the 'comboGroups' function from the `RcppAlgos` package should be used to generate group assignments. It is slightly faster to use the `comboGroups` function than it is to use `base` functions only. The default value, `TRUE`, uses this `comboGroups` function. If the `RcppAlgos` package or the `comboGroups` function change, set this argument to `FALSE` to ensure that this function for optimally assigning items to groups will still work.

<b>Works Cited</b>

Wood, J. 2021. RcppAlgos: High Performance Tools for Combinatorics and Computational Mathematics. R package version 2.4.3. <https://cran.r-project.org/web/packages/RcppAlgos/>.
