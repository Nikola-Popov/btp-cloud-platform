<!-- loio79b3c9b7701248fe83b81d4b15134e8d -->

# Display Authorization Trace



With this app you can enable an authorization trace for a business user. This helps you to analyze if any authorizations are missing or are insufficient.



## Key Features

You can use this app to:



-   Activate or deactivate a trace

-   Display authorization check results including already assigned authorizations and failed checks
-   Display all business roles granting access to selected fields and values

A maximum of 10.000 data sets is possible, therefore we recommend to consider this when defining the selection criteria, especially the date range.

The following authorization check statuses are possible:

****


<table>
<tr>
<th valign="top">

Status

</th>
<th valign="top">

Meaning

</th>
</tr>
<tr>
<td valign="top">

Successful

</td>
<td valign="top">

The authorization check was successful.

</td>
</tr>
<tr>
<td valign="top">

Failed

</td>
<td valign="top">

The authorization check failed.

</td>
</tr>
<tr>
<td valign="top">

Filtered

</td>
<td valign="top">

When reading an object, an authorization check is taking place and certain data is filtered out defined by a DCL \(Data Control Language\).

> ### Note:  
> When the *Authorization Check Status* is set to *Filtered*, no authorization check is carried out for any value. Instead, access filtering occurs. In this case, *No Value* is displayed for the corresponding restriction fields. Filtering means that the authorizations of the user for the specified restriction type/authorization object and for the specified field values are read and these authorization values are used as additional filter conditions during the selection of the business data. This way, the user only has access to the data for which he or she has appropriate authorizations.



</td>
</tr>
</table>

If an authorization check resulted in a *Failed* and *Filtered* status, you can check which business roles expose the affected restriction type. The root cause could be that the business user that has been checked is not assigned to the required business role or that the required value has not been maintained yet.

> ### Note:  
> The trace entries are deleted automatically within a certain time frame.



<a name="loio79b3c9b7701248fe83b81d4b15134e8d__supported_devices"/>

## Supported Device Types

-   Desktop

-   Tablet




<a name="loio79b3c9b7701248fe83b81d4b15134e8d__customer_component"/>

## Component for Customer Incidents

If you need support or experience issues, please report an incident under component `BC-SRV-APS-IAM`.

