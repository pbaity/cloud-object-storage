---

copyright:
  years: 2019, 2024
lastupdated: "2024-04-17"

keywords: activity, tracking, object storage, event, tutorial

subcollection: cloud-object-storage

content-type: tutorial
account-plan: lite
completion-time: 30m

---

{{site.data.keyword.attribute-definition-list}}

# Tracking {{site.data.keyword.cos_short}} events in {{site.data.keyword.at_short}}
{: #tracking-cos-events}
{: toc-content-type="tutorial"}
{: toc-completion-time="30m"}

Tracking {{site.data.keyword.cos_full}} events with {{site.data.keyword.at_full}} provides a record of what is happening with your data.
{: shortdesc}

This tutorial provides an introduction to capturing information regarding the events of your {{site.data.keyword.cos_short}} instance using {{site.data.keyword.at_short}}.

If you're not familiar with {{site.data.keyword.cos_full}}, you can quickly get an overview by [getting started with {{site.data.keyword.cos_full_notm}}](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage). Also, if you're not familiar with {{site.data.keyword.at_full}}, you may wish to check out how to [get started with {{site.data.keyword.at_short}}](/docs/activity-tracker?topic=activity-tracker-getting-started).

## Before you begin
{: #tracking-cos-events-prereqs}

If you are already managing instances of {{site.data.keyword.cos_short}} or {{site.data.keyword.at_short}}, you do not need to create more. However, as this tutorial will modify and configure the instance we are working with, make sure that any accounts or services are not being used in a production environment.

This tutorial will create a new bucket and a new instance of {{site.data.keyword.at_short}} in the process.  It is possible to associate an new or existing instance of {{site.data.keyword.at_short}} with an existing bucket through the bucket's configuration panel, but start fresh in this case.

For this tutorial, you need:
- An [{{site.data.keyword.cloud}} Platform account](https://cloud.ibm.com){: external}
- An [instance of IBM Cloud Object Storage](/objectstorage/create)
- To complete the steps to manage access to the service, your user ID needs **administrator platform permissions** to manage the {{site.data.keyword.at_full_notm}} service. You may have to contact a account administrator. The account owner can grant another user access to the account for the purposes of managing user access, and managing account resources. [Learn more](/docs/account?topic=account-userroles).
- Your user ID needs to be configured with the **service access writer role** at a minimum to create and manipulate buckets.

When naming buckets or objects, be sure to avoid the use of Personally Identifiable Information (PII). PII is information that can identify any user (natural person) by name, location, or any other means.
{: note}

## Create a new bucket
{: #at-tut-create-bucket}
{: step}

Navigate to your {{site.data.keyword.cos_short}} instance, and click the `Create bucket` button.

![Navigate to COS](images/at-tut-1-create-bucket.png)

## Create a custom bucket
{: #at-tut-custom-bucket}
{: step}

To create a custom bucket to provision the new {{site.data.keyword.at_short}} instance, click the `Customize your bucket` tile.

![Create a custom bucket](images/at-tut-2-custom-bucket.png)

## Name the new bucket
{: #at-tut-name-bucket}
{: step}

Give the bucket a memorable name.  In this case the new bucket will be called `tracked-files` and it is being created in the `us-east` region.

![Name the bucket](images/at-tut-3-name-bucket.png)

## Add {{site.data.keyword.at_short}}
{: #at-tut-add-at}
{: step}

Scroll down to the `Monitoring and activity tracking` section and toggle the radio button to `Enable activity tracking`.  Select an appropriate plan, and give the new instance a memorable name.  In this case, you are creating the instance in the same region as the bucket (`us-east`) so you should name the instance `US East AT` so you can easily find it later.

Track data events for both reading and writing.

![Add AT](images/at-tut-4-add-at.png)

## Find the new instance of {{site.data.keyword.at_short}}
{: #at-tut-find-at}
{: step}

Navigate back to the dashboard, and look for the new instance. Click it to open the {{site.data.keyword.at_short}} console.

![Find AT](images/at-tut-5-find-at.png)

## Launch the {{site.data.keyword.at_short}} interface
{: #at-tut-open-at}
{: step}

Now you can see some metadata about our new {{site.data.keyword.at_short}} instance (location, CRN, and so on).  Click on the ``View IBM Cloud Activity Tracker` button to launch the interface.

![Open AT](images/at-tut-6-open-at.png)


Notice that there's nothing here.  It will take a little while for the new instance to be associated with the bucket - while data operations (like reading or writing objects) are immediately consistent, operations that update the bucket's metadata (such as adding an {{site.data.keyword.at_short}} association) are eventually consistent and may take 15 minutes or so to propagate across the system.

![View AT](images/at-tut-7-empty-at.png)

## Trigger an event
{: #at-tut-view-bucket}
{: step}

Navigate back to your bucket.  When you open the bucket in the console it will trigger a listing, even though the bucket is empty. Behind the scenes, the console is sending a `GET bucket` request to list the objects, and {{site.data.keyword.at_short}} is going to log this listing event.

![View bucket](images/at-tut-8-view-bucket.png)

## View the {{site.data.keyword.at_short}} events
{: #at-tut-view-at}
{: step}

Now, assuming there has been enough time for the metadata to propagate, when you return to the {{site.data.keyword.at_short}} interface you will see some listing events.

![View AT](images/at-tut-9-view-at.png)

## Next steps
{: #at-tut-next-steps}

Congratulations, you've just set up a bucket with {{site.data.keyword.at_short}} enabled. Next, learn more about [how the {{site.data.keyword.at_short}} service itself routes events](/docs/activity-tracker?topic=activity-tracker-getting-started), all [the various events that {{site.data.keyword.cos_short}} can generate](/docs/cloud-object-storage?topic=cloud-object-storage-at-events), or how to integrate this to [provide end-to-end security for a cloud application](/docs/solution-tutorials?topic=solution-tutorials-cloud-e2e-security).
