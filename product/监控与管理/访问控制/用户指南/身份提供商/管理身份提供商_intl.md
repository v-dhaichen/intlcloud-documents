## Deleting SAML IdP

You can manage your IdPs via either CAM console or CAM API.

### Delete via console
1. Log in to the CAM console, and go to [Identity Provider](https://intl.cloud.tencent.com/login).
2. On the IdP list, select the IdP you want to delete and click **Delete** in the **Operation** column.
3. Confirm that you are deleting the right IdP, click **OK**.

### Delete via API

- (Optional) To list all IdP information in pages, call [ListSAMLProviders](https://intl.cloud.tencent.com/document/product/598/30386).
- (Optional) To get the details of a specific IdP, call [GetSAMLProvider](https://intl.cloud.tencent.com/document/product/598/30385).
- To delete an SAML IdP, call [Delete SAML Provider](https://intl.cloud.tencent.com/document/product/598/30387).

## Modifying SAML IdP

You can modify an IdP via either CAM console or CAM API.

### Modify via console
1. Log in to the CAM console, and go to [Identity Provider](https://intl.cloud.tencent.com/login).
2. From the IdP list, select the IdP you want to modify and click the IdP name to enter the detail page.
3. You can upload the metadata document to redefine the current IdP or download the current metadata document.

### Modify via API

Update the description or the metadata document of an SAML IdP.
- Call [UpdateSAMLProvider](https://intl.cloud.tencent.com/document/product/598/30384).

