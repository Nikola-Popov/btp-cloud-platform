<!-- loiod097ce26cb2d4b8fa9a597a5381cb3cb -->

# Migration from SAML Trust to OpenID Connect Trust with SAP Cloud Identity Services

To use or get the most out of some applications, such as SAP Build Work Zone and SAP Build Apps, your subaccount must use SAP Cloud Identity Services with OpenID Connect \(OIDC\) as the custom identity provider. This process helps you change an SAML trust configuration to an OIDC configuration with as little impact to your application users as possible, especially in productive subaccounts.

The goal of this process is as follows:

-   Preserve user records, including their authorizations, and also all user-related data in applications and services. User IDs don't change. We update the existing trust configuration instead of creating a new one.

-   Preserve role collection mappings to groups or other attributes.

-   Ensure that applications receive exactly the same information about users as they did before. We provide guidance and verification steps for when you reconfigure authentication along the chain of subaccount, SAP Cloud Identity Services tenant, and potentially corporate identity provider.


> ### Caution:  
> You could achieve a similar result by deleting your current SAML trust configuration and setting up a new trust with OIDC. However, this method can cause an interruption in the service to your business users. Deleting the trust deletes any local shadow users in the subaccount and their role collection assignments. You would need to re-create those users and their role collection assignments. You would also permanently lose any connection to application data for those users. The internal IDs of the re-created users will never be the same as with the original trust configuration.



<a name="loiod097ce26cb2d4b8fa9a597a5381cb3cb__section_u3t_xv1_3xb"/>

## Restrictions

In the SAP BTP cockpit under *Custom Identity Provider for Applications*, there are no trust configurations with protocol OpenID Connect and no more than one with SAML.

> ### Note:  
> The content in this section is not relevant for China \(Shanghai\) and Government Cloud \(US\) regions.



<a name="loiod097ce26cb2d4b8fa9a597a5381cb3cb__section_gvh_gkj_gxb"/>

## Architecture

You have one of the following configurations:

-   You've already configured SAP Cloud Identity Services as a trusted identity provider, but with SAML. Optionally the SAP Cloud Identity Services tenant trusts a corporate identity provider.

    For this case, you don't change the architecture, only the protocol between the subaccount and the SAP Cloud Identity Services tenant. If you use a corporate identity provider, configure the new SAP Cloud Identity Services application to authenticate with it.

      
      
    **Update of Existing Trust Configuration for SAP Cloud Identity Services**

    ![](images/IAS_protocol_switch_a732ec6.png "Update of Existing Trust Configuration for SAP Cloud Identity Services")

-   You've connected your corporate identity provider directly with your subaccount as the trusted identity provider with SAML.

    For this case, you insert trust to SAP Cloud Identity Services in between and configure SAP Cloud Identity Services as a proxy for your corporate identity provider.

      
      
    **Insertion of SAP Cloud Identity Services in Trust Chain of Identity Providers**

    ![](images/Injection_of_IAS_Between_Corp_IDP_db96a95.png "Insertion of SAP Cloud Identity Services in Trust Chain of Identity Providers")




<a name="loiod097ce26cb2d4b8fa9a597a5381cb3cb__section_dd1_gnj_gxb"/>

## Risks and Downtime

Expect a downtime between the time when you start the migration and when you've re-established and configured the chain of trust with your identity providers, including the new SAP Cloud Identity Services application representing your subaccount.

> ### Recommendation:  
> Practice this procedure in your dev or test subaccounts before carrying it out in your productive subaccounts. Practice helps you to learn how the migration works, enabling you to minimize the risk of misconfiguration and downtime in your productive environments.
> 
> If you use the same SAP Cloud Identity Services tenant for nonproductive and productive subaccounts, the integration between SAP Cloud Identity Services and your corporate identity provider is already complete as part of the preparation for the nonproductive subaccounts. This setup reduces the risk and downtime for productive subaccounts.

We provide a rollback function if you encounter any problems.

For more information, see [Restore SAML Trust Configuration](restore-saml-trust-configuration-21d86cf.md).



<a name="loiod097ce26cb2d4b8fa9a597a5381cb3cb__section_uvj_hnj_gxb"/>

## Process Overview

1.  Prepare for the migration to minimize the downtime starting in step 2.

    1.  Collect and save the user data with the existing SAML trust. After the migration, use this information to verify that everything works correctly.

    2.  If you use a corporate identity provider and it isn't yet trusted by your SAP Cloud Identity Services tenant, establish trust now.


    For more information, see [Prepare for Migration from SAML Trust to OpenID Connect](prepare-for-migration-from-saml-trust-to-openid-connect-269f60d.md).

2.  Migrate the subaccount's trust configuration, updating the existing SAML trust to an OIDC trust with SAP Cloud Identity Services.

    For more information, see [Migrate from SAML Trust Configuration to OpenID Connect Trust with SAP Cloud Identity Services](migrate-from-saml-trust-configuration-to-openid-connect-trust-with-sap-cloud-identity-s-827ae66.md).

3.  Configure your new OIDC application for your subaccount.

    Adjust the user subject and any attributes used by your new application in SAP Cloud Identity Services to match your old trust configuration.

    If you use a corporate identity provider, configure the application in SAP Cloud Identity Services to use the corporate identity provider for user authentication.

    For more information, see [Configuration of SAP Cloud Identity Services After Migration from SAML to OIDC](configuration-of-sap-cloud-identity-services-after-migration-from-saml-to-oidc-1fa7273.md).

4.  Verify that user authentication works as before the migration.

    For more information, see [Test the Trust Configuration After the Migration](test-the-trust-configuration-after-the-migration-edc7c42.md).


