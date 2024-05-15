<!-- loio13359c4e63994b3eaee1d1abe35049c8 -->

# Delete Spaces Using the Cloud Foundry Command Line Interface

Use the `cf delete-space` command to delete spaces in your Cloud Foundry organization using the Cloud Foundry Command Line Interface \(cf CLI\).



<a name="loio13359c4e63994b3eaee1d1abe35049c8__prereq_zt3_mzc_wbb"/>

## Prerequisites

-   You have the Org Manager role in the organization from which you want to delete a space. For more information about roles and permissions, see [https://docs.cloudfoundry.org/concepts/roles.html](https://docs.cloudfoundry.org/concepts/roles.html).
-   Download and install the cf CLI and log on to Cloud Foundry. For more information, see [Download and Install the Cloud Foundry Command Line Interface](download-and-install-the-cloud-foundry-command-line-interface-4ef907a.md) and [Log On to the Cloud Foundry Environment Using the Cloud Foundry Command Line Interface](log-on-to-the-cloud-foundry-environment-using-the-cloud-foundry-command-line-interface-7a37d66.md).




<a name="loio13359c4e63994b3eaee1d1abe35049c8__steps_mv3_csm_qz"/>

## Procedure

1.  Make sure that you are in the Cloud Foundry organization you want to delete a space in.

    ```
    cf target -o ORG
    ```

    To get a list of your organizations, call `cf orgs`.

2.  Enter the following string, specifying a name for the space, and the name of the organization:

    ```
    cf delete-space SPACE [-o ORG] [-f]
    ```

    To get the list of your spaces, call `cf spaces`.


**Related Information**  


[Create Spaces Using the Cloud Foundry Command Line Interface](create-spaces-using-the-cloud-foundry-command-line-interface-a2e5e29.md "Use the cf create-space command to create spaces in your Cloud Foundry organization using the Cloud Foundry Command Line Interface (cf CLI).")

[Delete Spaces Using the Cockpit](delete-spaces-1eb6a09.md "Delete spaces in your Cloud Foundry org using the SAP BTP cockpit.")

