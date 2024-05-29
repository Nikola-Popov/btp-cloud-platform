<!-- loio1f04ad22db0147b99ebc476708b749b6 -->

# Creating the Job Template

An *Application Job Template* refers to an application job catalog entry and contains values for some or all selection fields. It can be thought of as a variant of an application job catalog. In the simplest case, a job template doesn't contain any values for the selection fields. In this case, the selection fields are prefilled with their initial values \(such as 0 if the selection field is of type integer\). An application job catalog entry can have more than one application job template. The job template is the entity that can be scheduled in the *Application Jobs* app. In the scheduling dialog, the selection fields appear and are prefilled with the values defined in the template. They can be overwritten by the user. Scheduling an application job template then results in an application job.

You can create a job template in the ABAP development tools for Eclipse. For more information, see [Creating Application Job Templates](https://help.sap.com/docs/abap-cloud/abap-development-tools-user-guide/creating-application-job-templates?version=sap_btp). The creation of a job template follows the same technical rules as a *Job Catalog Entry* as described in [Creating the Job Catalog Entry](creating-the-job-catalog-entry-1cff59e.md).

The following code example shows a console application that generates the minimal number of required development objects: One *Job Catalog* entry and one related *Job Template*.

> ### Sample Code:  
> ```abap
> CLASS zcl_test_apj_simple_obj_gen DEFINITION
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
> 
> CLASS zcl_test_apj_simple_obj_gen IMPLEMENTATION.
> 
>   METHOD if_oo_adt_classrun~main.
> 
>     CONSTANTS lc_catalog_name      TYPE cl_apj_dt_create_content=>ty_catalog_name  VALUE 'ZTEST_MY_SIMPLE_JOB'.
>     CONSTANTS lc_catalog_text      TYPE cl_apj_dt_create_content=>ty_text          VALUE 'My first simple application job'.
>     CONSTANTS lc_class_name        TYPE cl_apj_dt_create_content=>ty_class_name    VALUE 'ZCL_TEST_APJ_SIMPLE'.
> 
>     CONSTANTS lc_template_name     TYPE cl_apj_dt_create_content=>ty_template_name VALUE 'ZTEST_MY_SIMPLE_JOB_TEMPL'.
>     CONSTANTS lc_template_text     TYPE cl_apj_dt_create_content=>ty_text          VALUE 'My first simple job template'.
> 
>     CONSTANTS lc_transport_request TYPE cl_apj_dt_create_content=>ty_transport_request VALUE 'Y11K900361'.
>     CONSTANTS lc_package           TYPE cl_apj_dt_create_content=>ty_package           VALUE 'Z_D028092_APJ_MAIN'.
> 
>     DATA(lo_dt) = cl_apj_dt_create_content=>get_instance( ).
> 
>     " Create job catalog entry (corresponds to the former report incl. selection parameters)
>     " Provided implementation class iv_class_name shall implement two interfaces:
>     " - if_apj_dt_exec_object to provide the definition of all supported selection parameters of the job
>     "   (corresponds to the former report selection parameters) and to provide the actual default values
>     " - if_apj_rt_exec_object to implement the job execution
>     TRY.
>         lo_dt->create_job_cat_entry(
>             iv_catalog_name       = lc_catalog_name
>             iv_class_name         = lc_class_name
>             iv_text               = lc_catalog_text
>             iv_catalog_entry_type = cl_apj_dt_create_content=>class_based
>             iv_transport_request  = lc_transport_request
>             iv_package            = lc_package
>         ).
>         out->write( |Job catalog entry created successfully| ).
> 
>       CATCH cx_apj_dt_content INTO DATA(lx_apj_dt_content).
>         out->write( |Creation of job catalog entry failed: { lx_apj_dt_content->get_text( ) }| ).
>     ENDTRY.
> 
>     " Create job template (corresponds to the former system selection variant) which is mandatory
>     " to select the job later on in the Fiori app to schedule the job
>     DATA lt_parameters TYPE if_apj_dt_exec_object=>tt_templ_val.
> 
>     NEW zcl_test_apj_simple( )->if_apj_dt_exec_object~get_parameters(
>       IMPORTING
>         et_parameter_val = lt_parameters
>     ).
> 
>     TRY.
>         lo_dt->create_job_template_entry(
>             iv_template_name     = lc_template_name
>             iv_catalog_name      = lc_catalog_name
>             iv_text              = lc_template_text
>             it_parameters        = lt_parameters
>             iv_transport_request = lc_transport_request
>             iv_package           = lc_package
>         ).
>         out->write( |Job template created successfully| ).
> 
>       CATCH cx_apj_dt_content INTO lx_apj_dt_content.
>         out->write( |Creation of job template failed: { lx_apj_dt_content->get_text( ) }| ).
>         RETURN.
>     ENDTRY.
> 
>   ENDMETHOD.
> 
> ENDCLASS.
> 
> ```

**Related Information**  


[Setting up the Authorizations](setting-up-the-authorizations-bb559a5.md "Some further activities in ADT and in the administrator’s launchpad are necessary to be able to schedule the job template in the Fiori app Application Jobs.")

