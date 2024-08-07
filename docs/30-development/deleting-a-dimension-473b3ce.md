<!-- loio473b3cef24484784bd9df78b31c64990 -->

# Deleting a Dimension

Use method `DELETE` to delete a dimension.

> ### Caution:  
> Changing the initial set of configurations has implications. Before proceeding with any change, familiarize yourself with the warnings in [Units of Measurement](units-of-measurement-8961c2c.md).



<a name="loio473b3cef24484784bd9df78b31c64990__section_u5d_g4v_plb"/>

## Import Parameters

****


<table>
<tr>
<th valign="top">

Parameter Name

</th>
<th valign="top">

Value Help

</th>
</tr>
<tr>
<td valign="top">

DIMID

</td>
<td valign="top">

Dimension key

</td>
</tr>
</table>



<a name="loio473b3cef24484784bd9df78b31c64990__section_fkc_ddv_plb"/>

## Export Parameters

****


<table>
<tr>
<th valign="top">

Parameter Name

</th>
<th valign="top">

Value Help

</th>
</tr>
<tr>
<td valign="top">

ERROR

</td>
<td valign="top">

`Space`: No error

`‘X’`: Save error

</td>
</tr>
</table>

> ### Note:  
> Class exception `CX_UOM_ERROR` is raised to check the integrity of the data import parameters.

> ### Sample Code:  
> ```abap
> CLASS zcl_uom_dimension_delete_test DEFINITION 
>   PUBLIC 
>   FINAL 
>   CREATE PUBLIC . 
>  
>   PUBLIC SECTION. 
>     INTERFACES if_oo_adt_classrun. 
>   PROTECTED SECTION. 
>   PRIVATE SECTION. 
> ENDCLASS. 
>  
> CLASS zcl_uom_dimension_delete_test IMPLEMENTATION. 
>   METHOD if_oo_adt_classrun~main.  
>   
>  DATA(lo_dim) = cl_uom_dim_maintenance=>get_instance( ).
>  
>     TRY.
>         lo_dim->delete( EXPORTING dimid = 'ZNEWDI'
>                         IMPORTING error = DATA(lv_error) ).
>       CATCH cx_uom_error INTO DATA(lo_error).
>         out->write( |Exception raised| ).
>         out->write( lo_error->get_text( ) ).
>     ENDTRY.
>     IF lv_error = abap_true.
>       out->write( |Error occurred while deleting the data from the database| ).
>     ENDIF.
>   ENDMETHOD. 
> ENDCLASS.
> 
> 
> ```

