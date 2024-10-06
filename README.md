SiteLink README.md  

SiteLink Documentation
======================

*   [SiteLink Operator](#sitelink)
*   [SiteLink Path Operator](#sitelink_path)
*   [SiteLink Configuration File (sitelink.ini)](#sitelink-ini)

* * *

SiteLink Operator
-----------------

The sitelink operator is the root operator for all of the operators provided by this class by returning the URL string for the given input value.

### Features

*   Link between multiple domains hosted on the same eZ Publish install
    *   Provide a preferred host based on siteaccess
*   Force all generate URLs to be absolute
    *   At the operator call or in the sitelink.ini file
    *   Override sitelink.ini setting at operator call
*   Allow custom functionality for the generated URL based on node class and attribute datatype (based on if install is a multisite)
    *   Provide a preferred link type for the class
    *   Prevent the provided page from linking to itself (currently the operator will return an empty string)
    *   Override the default specified datatype handler php class
*   Override the default datatype handler php class for a specified attribute datatype with a new one
    *   requires a php interface based class
*   Allow a role for the current user to determine the siteaccess to be used in the generated URL string
*   Support for the PathPrefixExclude ini setting

### Usage

input|sitelink(\[ parameters \[, absolute \] \])

input

The available input values for the operator are:

`node_id`

An integer value representing the id of a node.

`object_id`

An integer value representing the id of an object. If this input option is desired, the node\_id parameter **must** be set to `false`.

`node`

An object value that is a content object tree node.

`object`

An object value that is a content object.

`uri_string`

A string which is a relative or absolute URI.

parameters `(array | boolean | integer | string)`

The parameters to be used in the processing of `input`. When this value is not an `array`, it is given to be the `quotes` value of the available associative array parameters. Available values for the associative array are:

`absolute` \[false\]

Specify if the returned URL string should be an absolute or relative URL.

*   `boolean` (true/false)
*   `integer` (1/0)
*   `string` (yes/no)

`debug` \[false\]

Allow internal PHP debugging to be used for a single use of sitelink without the debug output for all calls to sitelink.

\*`hash` \[false\]

The URL fragment (hash) to append to the returned URL string.

`node_id` \[true\]

Specify that the integer value given as an input is a node\_id or contentobject\_id

`quotes` \[true\]

Should the returned URL string be quoted.

*   `boolean` (true/false)
*   `integer` (1/0)
*   `string` (yes/no)

\*`query` \[false\]

The URL query string to append to the return URL string. This can be either an associative array or a string.

`user_parameters` \[false\]

The user parameters to append to the returned URL string. This can be either an associative array or a string.

\* This parameter has not be made functional.

absolute `(boolean | integer | string)`

Specify if the returned URL string should be an absolute or relative URL. If ForceAbsoluteURL is enabled, setting this value to `false` will not override the setting. In order to override this setting, the `absolute` parameter _must_ be set in parameters array.

*   `boolean` (true/false)
*   `integer` (1/0)
*   `string` (yes/no)

SiteLink Path Operator
----------------------

The sitelink\_path operator provides a correct path for the given input.

### Features

*   Provide a correct path for the given page
    *   currently only node based pages are functional
*   Disable a page from linking in the path
    *   Based on node id or object id

### Usage

input|sitelink\_path(\[ absolute \])

input

see input for the SiteLink operator

absolute `(boolean | integer | string)`

Specify if the returned URL string should be an absolute or relative URL.

*   `boolean` (true/false)
*   `integer` (1/0)
*   `string` (yes/no)

SiteLink Configuration File (sitelink.ini)
------------------------------------------

### \[OperatorSettings\]

DefaultLinkType \[ **internal** | external |download \]

Sets the default link type for all SiteLink classes. This setting is related to the class block LinkTypeList settings.

ForceAbsoluteURL \[ **disabled** | enabled \]

Force all generate URLs to be absolute.

HostOverride \[ **disabled** | enabled \]

Allows the site.ini HostMatchMapItems setting to be overridden to specify a default hostname when more than one hostname matches a siteaccess

RoleList

The list of role\_id/siteaccess pairs for the RoleOverride feature.

RoleList\[_role\_id_\]=_siteaccess_

RoleOverride \[ **disabled** | enabled \]

Allow a role for the current user to determine the siteaccess to be used in the generated URL string

SiteAccess

The list of siteaccess/hostname pairs for the HostOverride feature.

SiteAccess\[_siteacces\_name_\]=_hostname_

SiteLinkClassList

The list of classes to be used for custom URL generation.

Default Classes:

*   link
*   file
*   image
*   banner

### \[SiteLinkPathSettings\]

DisableNodeID \[ **disabled** | enabled \]

Prevents the node in the generated path from being a link

DisableObjectID \[ **disabled** | enabled \]

Prevents all node instances of the object in the generated path from being a link

NodeIDList

The list of node ids to disable

ObjectIDList

The list of object ids to disable

### \[DataTypeSettings\]

ClassList

The list of PHP classes to be used with a specific attribute datatype.

ClassList\[_attribute\_datatype_\]=_php\_class_

### \[_class\_identifier_\]

A custom block where each block as a corresponding entry in the \[OperatorSettings\]\[SiteLinkClassList\] setting.

DataTypeClass

Specifiy an override data type class to use

DefaultLinkType

Used to override the operator setting for a class

LinkTypeList

Specifiy the attribute identifier to use for each link type. Example:

LinkTypeList\[internal\]=internal\_link

SelfLinking \[ disabled | **enabled** \]

Prevent an input of this class from linking to itself (currently the operator will return an empty string)
