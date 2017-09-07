# Add Version

To see the available versions of a site go to the [Sites module](http://admin.daspanel.site/sites/)

[![Daspanel site versions](../img/site-versions.png)](../img/site-versions.png)

1. Click the **third bullet** to display the version management area of the chosen site.

The site card will be changed to the version management area:

[![Daspanel site versions tab](../img/site-versions-area.png)](../img/site-versions-area.png)

1. Click the **MANAGE** buttom to go the management page.

On the next page you will see a list of all the existing versions for the site:

[![Daspanel site versions add](img/site-versions-add1.png)](img/site-versions-add1.png)

1. Click the "**+**" button at the top right of the versions page.

You'll see a new page to add a new version for the site:

[![Daspanel site versions add page](img/site-versions-add2.png)](img/site-versions-add2.png)

1. **Description**: Write an description for the new version
2. **Tag**: Ignored for now. It will be used in the future.
3. **Engine**: Select the type of engine that will be used by this version

    !!! note ""
        The engine of the website is nothing more than the programming language 
        that is used to create it. If your site needs PHP choose the engine with 
        the most appropriate version. If the site is made only with HTML and 
        Javascript choose the option *Static*.

4. **Type**: Select the type of this version

    !!! note ""
        The options of this choice vary depending on the engine chosen for the 
        site in the previous option. All engines will have at least the 
        *Generic* option.

        If the engine of your site is not *Static* it is important to choose the 
        correct type because it is through this information that Daspanel will 
        properly configure the HTTP server for the site being created.

5. Create the new site version by clicking the **CREATE VERSION** button.
6. Or click the **left arrow** ![Alt](/help/sites/img/back-arrow.png "Back") at the top of 
the screen to return without saving anything.

Once the operation is successfully completed the list of versions is updated:

[![Daspanel site versions add result](img/site-versions-add3.png)](img/site-versions-add3.png)

Now with the new version that has been added you can:

* [Set Active version](/help/sites/versions/activate)
* [Edit version](/help/sites/versions/edit)
* [Delete version](/help/sites/versions/delete)
* [Preview version](/help/sites/versions/preview)

