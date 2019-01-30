# Salesforce Lookup Component (Aura version)
Lightning Web Component version is available [here](https://github.com/pozil/sfdc-ui-lookup-lwc).

<p align="center">
    <img src="screenshots/lookup-animation.gif" alt="Lookup animation"/>
</p>

<img src="screenshots/dropdown-open.png" alt="Lookup with dropdown open" width="350" align="right"/>

## About
This is a generic &amp; customizable lookup component built using Salesforce Lightning (Aura) and [SLDS](https://www.lightningdesignsystem.com) style.<br/>
It does not rely on third party libraries and you have full control over its datasource.

<b>Features</b>

The lookup component provides the following features:
- customizable data source that can return mixed sObject types
- single or multiple selection mode
- client-side caching & request throttling
- built-in server request rate limit mechanism

<p align="center">
    <img src="screenshots/selection-types.png" alt="Multiple or single entry lookup"/>
</p>

## Documentation
The lookup component is documented using Aura documentation.<br/>
You can access it from this URL (replace the domain):<br/>
https://<b>&lt;YOUR_DOMAIN&gt;</b>.lightning.force.com/docs/component-library/bundle/c:Lookup/documentation

Follow these steps in order to use the lookup component:

### 1) Write the search endpoint

Implement an Apex `@AuraEnabled` method (`SampleLookupController.search` in our samples) that returns the search results as a `List<LookupSearchResult>`.
The method name can be different but it needs to match this signature:

```apex
@AuraEnabled
public static List<LookupSearchResult> search(String searchTerm, List<String> selectedIds) {}
```

### 2) Handle the `search` event and pass the results to the lookup

The lookup component exposes an `onSearch` component event that is fired when a search needs to be performed on the server-side.
The parent component that contains the lookup must handle the `onSearch` event:
```xml
<c:Lookup aura:id="lookup" selection="{!v.selection}" onSearch="{!c.lookupSearch}" label="Search"/>
```

The event handler should do the following:
```js
lookupSearch : function(component, event, helper) {
    // Get the Apex server-side action associated with this search (`search` in our samples)
    const serverSearchAction = component.get('c.search');
    // Passes the action to the lookup component by calling the `search` aura method
    component.find('lookup').search(serverSearchAction);
}
```


## Salesforce DX setup instructions
Deploy the sample application with Salesforce DX by clicking on this button:

[![Deploy](https://deploy-to-sfdx.com/dist/assets/images/DeployToSFDX.svg)](https://deploy-to-sfdx.com)


## Sample application
The default installation installs the lookup component and a sample application available under this URL (replace the domain):<br/>
https://<b>&lt;YOUR_DOMAIN&gt;</b>.lightning.force.com/c/SampleLookupApp.app

If you wish to install the project without the sample application, edit `sfdx-project.json` and remove the `src-sample` path.
