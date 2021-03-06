# Installing patches on the @product-ver@ WAR [](id=installing-patches-on-the-liferay-de-war)

If you
[installed @product@ manually](/discover/deployment/-/knowledge_base/7-1/installing-liferay-manually)
as a WAR file on a supported application server, you must apply patches to the
WAR file and supporting files and re-deploy them. This tutorial shows you how to
do that.

## Prerequisites [](id=prerequisites)

Download the necessary artifacts from the 
[Customer Portal:](https://web.liferay.com/group/customer/dxp/downloads/7-1)

- @product@ WAR file (`liferay-dxp-[version].war`)
- Dependencies ZIP file (`liferay-dxp-dependencies-[version].zip`)
- OSGi JARs ZIP file (`liferay-dxp-osgi-[version].zip`) 
- [Latest Patching Tool](https://web.liferay.com/group/customer/dxp/downloads/digital-enterprise/patching-tool)

## Install the patch on the @product@ WAR and artifacts [](id=how-to-install-a-fix-pack-on-the-liferay-war)

1.  Create an arbitrary folder. Unzip the dependency artifacts and the 
    Patching Tool into it. The folder contents should look like this:

    - `[patching-home]/`
        - `liferay-dxp-dependencies-[version]/` &larr; Unzipped Dependencies
        - `osgi/` &larr; Unzipped OSGi JARs
        - `patching-tool/` &larr; Unzipped Patching Tool
        - `liferay-dxp-[version].war/` &larr; @product@ WAR File

2.  Create the default profile configuration file in the Patching Tool folder:
    `patching-home/patching-tool/default.properties`. The contents should look
    like this:

        patching.mode=binary
        war.path=../../patching-home/liferay-dxp-[version].war
        global.lib.path=../../patching-home/liferay-dxp-dependencies-[version]
        liferay.home=../../patching-home

    If you're using a different OSGi folder structure, you can specify it as
    the [Patching Tool Advanced Configuration](/discover/deployment/7-1/knowledge_base/patching-tool-advanced-configuration)
    documentation describes: 
	
        module.framework.core.path=/osgi-home/osgi/core
        module.framework.marketplace.path=/osgi-home/osgi/marketplace
        module.framework.modules.path=/osgi-home/osgi/modules
        module.framework.portal.path=/osgi-home/osgi/portal
        module.framework.static.path=/osgi-home/osgi/static	

3.  Download the patch (fix pack or hotfix) to install and put it in a folder 
    called `patches` in your Patching Tool folder:

        [patching-home]/patching-tool/patches 

4.  Execute the Patching Tool's `info` command:

        /patching-home/patching-tool> patching-tool info
        Loading product and patch information...
        Product information:
          * installation type: binary
          * build number: 7110
          * service pack version:
            - available SP version: Not available
            - installable SP version: Not available
          * patching-tool version: 2.0.8
          * time: 2018-09-12 18:30Z
          * host: 91WRQ72 (8 cores)
          * plugins: no plugins detected

        Currently installed patches: -
        Available patches: dxp-2-7110

        Detailed patch list:
          [ I] dxp-2-7110 :: Currently not installed; Will be installed. :: Built for LIFERAY

5.  Install the patch. 

        /patching-home/patching-tool> patching-tool.sh  install
        One patch is ready to be installed. Applying dxp-2...
        Cleaning up: [1%..10%..20%..30%..40%..50%..60%..70%..80%..90%..100%]
        Installing patches: [1%..10%..20%..30%..40%..50%..60%..70%..80%..90%...100%]
        The installation was successful. One patch is installed on the system.

Great! You have successfully patched the artifacts, and they are ready to be
deployed on any supported Application Server.

## Related Topics [](id=related-topics)

[Patching Tool Advanced Configuration](/discover/deployment/-/knowledge_base/7-1/patching-tool-advanced-configuration)

[Deploying @product@](/discover/deployment/-/knowledge_base/7-1/deploying-product)
