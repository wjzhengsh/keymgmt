---

copyright:
  years: 2017
lastupdated: "2017-07-10"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Troubleshooting

Here are the answers to common troubleshooting questions about using {{site.data.keyword.keymanagementservicefull}}.
{: shortdesc}

## Unable to create or delete keys
{: unabletomanagekeys}

If you cannot perform {{site.data.keyword.keymanagementserviceshort}} actions, verify that you have the correct authorization.

### Symptoms

When you access the {{site.data.keyword.keymanagementserviceshort}} user interface, you cannot view the options to add or delete keys.

### Resolving the problem

Verify with your space manager that you are assigned the correct role in the applicable space. For more information about roles, see [Auditing keys and access](https://console.bluemix.net/docs/services/keymgmt/managing.html#viewkeyassignments).

## Convert from beta to general assembly (GA)
{: ts_planconversion}

Beta users need to change to the standard pricing model to continue to use the {{site.data.keyword.keymanagementserviceshort}} service.

### Symptoms

If you are a beta user, you need to change your pricing plan to the tiered pricing model to continue storing keys in {{site.data.keyword.keymanagementserviceshort}}.

### Resolving the problem

The {{site.data.keyword.keymanagementserviceshort}} service has two pricing models: lite and graduated tiered. As an org or space manager, verify that the graduated tiered model has been selected. If you do not want to migrate to the tiered model, ensure that all keys and service instances are removed before deprecation. [See the {{site.data.keyword.keymanagementserviceshort}} general assembly announcement for more information ![External link icon](../../icons/launch-glyph.svg "External link icon")]("https://www.ibm.com/blogs/bluemix/2016/12/dallas-key-protect-ga/"){: new_window}.

To change the pricing plan:

1. Go to the {{site.data.keyword.keymanagementserviceshort}} user interface and select the **Plans** tab.
2. Select **Graduated Tier Pricing**.
    The breakdown of cost to active keys that are used per month appears in a table. The tiered model calculates pricing based on the number of active keys per month at the account level.
3. To confirm the plan change, click **Save**.

## Getting help and support for {{site.data.keyword.keymanagementserviceshort}}
{: ts_gettinghelp}

If you have problems or questions when you are using {{site.data.keyword.keymanagementservicefull_notm}}, you can get help by searching for information or by asking questions through a forum. You can also open a support ticket.

When you are using the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.IBM_notm}} {{site.data.keyword.Bluemix_notm}} development teams.

- If you have technical questions about {{site.data.keyword.keymanagementserviceshort}}, post your question on [Stack Overflow ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://stackoverflow.com/search?q=key-protect+ibm-bluemix){: new_window} and tag your question with "ibm-bluemix" and "key-protect".
- For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/answers/topics/key-protect/?smartspace=bluemix){: new_window} forum. Include the "bluemix"
and "key-protect" tags.

See [Getting help ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/support/index.html#getting-help){: new_window} for more details about using the forums.

For information about opening an {{site.data.keyword.IBM_notm}} support ticket, or about support levels and ticket severities, see [Contacting support ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/support/index.html#contacting-support){: new_window}.
