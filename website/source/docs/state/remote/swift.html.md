---
layout: "remotestate"
page_title: "Remote State Backend: swift"
sidebar_current: "docs-state-remote-swift"
description: |-
  Terraform can store the state remotely, making it easier to version and work with in a team.
---

# swift

Stores the state as an artifact in [Swift](http://docs.openstack.org/developer/swift/).

-> **Note:** Passing credentials directly via configuration options will
make them included in cleartext inside the persisted state. Use of
environment variables is recommended.

## Example Usage

```
terraform remote config \
  -backend=swift \
  -backend-config="path=terraform_state"
```

## Example Referencing

```
data "terraform_remote_state" "foo" {
  backend = "swift"
  config {
    path = "terraform_state"
  }
}
```

## Configuration variables

The following configuration options are supported:

 * `auth_url` - (Required) The Identity authentication URL. If omitted, the
   `OS_AUTH_URL` environment variable is used.

 * `path` - (Required) The path where to store `terraform.tfstate`.
 * `user_name` - (Optional) The Username to login with. If omitted, the
   `OS_USERNAME` environment variable is used.

 * `user_id` - (Optional) The User ID to login with. If omitted, the
   `OS_USER_ID` environment variable is used.

 * `password` - (Optional) The Password to login with. If omitted, the
   `OS_PASSWORD` environment variable is used.

 * `region_name` (Required) - The region in which to store `terraform.tfstate`. If
   omitted, the `OS_REGION_NAME` environment variable is used.

 * `tenant_id` (Optional) The ID of the Tenant (Identity v2) or Project
   (Identity v3) to login with. If omitted, the `OS_TENANT_ID` or
   `OS_PROJECT_ID` environment variables are used.

 * `tenant_name` - (Optional) The Name of the Tenant (Identity v2) or Project
   (Identity v3) to login with. If omitted, the `OS_TENANT_NAME` or
   `OS_PROJECT_NAME` environment variable are used.

 * `domain_id` - (Optional) The ID of the Domain to scope to (Identity v3). If
   If omitted, the following environment variables are checked (in this order):
   `OS_USER_DOMAIN_ID`, `OS_PROJECT_DOMAIN_ID`, `OS_DOMAIN_ID`.

 * `domain_name` - (Optional) The Name of the Domain to scope to (Identity v3).
   If omitted, the following environment variables are checked (in this order):
   `OS_USER_DOMAIN_NAME`, `OS_PROJECT_DOMAIN_NAME`, `OS_DOMAIN_NAME`,
   `DEFAULT_DOMAIN`.

 * `insecure` - (Optional) Trust self-signed SSL certificates. If omitted, the
   `OS_INSECURE` environment variable is used.

 * `cacert_file` - (Optional) Specify a custom CA certificate when communicating
   over SSL. If omitted, the `OS_CACERT` environment variable is used.

 * `cert` - (Optional) Specify client certificate file for SSL client
   authentication. If omitted the `OS_CERT` environment variable is used.

 * `key` - (Optional) Specify client private key file for SSL client
   authentication. If omitted the `OS_KEY` environment variable is used.