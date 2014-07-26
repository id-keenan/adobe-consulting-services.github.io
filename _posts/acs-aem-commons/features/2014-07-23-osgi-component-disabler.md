---
layout: acs-aem-commons_feature
title: OSGi Component Disabler
description: Disable OSGi Components as part of your build
date: 2014-07-23
thumbnail: /images/osgi-component-disabler/thumbnail.png
feature-tags: administration
tags: acs-aem-commons-features new
categories: acs-aem-commons features
initial-release: 1.7.0
---

## Purpose

The OSGi Component Disabler allows you to shutdown OSGi services and Components by configuration, but only after they have been started.

Some AEM components are interfere or simply be unneccessary for an implementation but cannot be turned off soley via configuration (or no configuration). The feature allows these OSGi Services and Components to be disabled as part of your applications configuration.


## Description

In Apache Felix the state of components and services is not persisted across restarts of its containing bundle.

For example, when you have a Bundle S containing a service S, and you manually stop the service S; after a deactivate and activate of the bundle the service S is up again.
 
This service allows you to specify the names of components, which shouldn't be running. Whenever an OSGI service event is fired, which services checks the status of this components and stops them if required.

Note 1: The component is always started, but this service takes care, that it is stopped immediately after. So if a behaviour you don't like already happens during the activation of this service, you cannot prevent it using the mechanism here.

Note 2: Using this service should always be considered as a workaround. The primary focus should be to fix the component you want to disable, so it's no longer required to disable it. If this component is part of Adobe AEM please raise a Daycare ticket for it.

## How to Use


* Define a `sling:OsgiConfig`'s

`/apps/mysite/config/com.adobe.acs.commons.util.impl.ComponentDisabler.xml`

{% highlight xml %}
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0"
    xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="sling:OsgiConfig"
    components="[pid1,pid2]"
    />
{% endhighlight %}     

`components` is an array of the OSGi component PIDs to disable.