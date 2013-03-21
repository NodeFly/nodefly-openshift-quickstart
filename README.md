# Nodefly on OpenShift
This git repository helps you to setup Nodefly and to showcases a working configuration of the Nodefly agent.

## Running on OpenShift
Create a Nodefly account at http://apm.nodefly.com/.

Sign up for OpenShift Online at http://openshift.redhat.com/ and set up you local development machine with the `rhc` command-line tools  by running `sudo gem install rhc` and `rhc setup`.

Create a node-0.6 application (you can call your application whatever you want) and change into the application directory.  We'll use the application name "nodefly" in this example:

    rhc app create nodefly nodejs-0.6 --from-code https://github.com/openshift/nodefly-openshift-quickstart.git
    cd nodefly

###Installation###

Make sure that the `nodefly` npm module has been added as a dependency in your application's `package.json` file:

    npm install -S nodefly

###Configuration###
Configure your `server.js` file with your NodeFly developer key, available on the [NodeFly howto page](http://nodefly.com/#howto):

    var app_name = process.env.OPENSHIFT_APP_NAME || 'local_development',
        host_url = process.env.OPENSHIFT_APP_DNS  || 'localhost',
        gear_id = process.env.OPENSHIFT_GEAR_UUID || 1,
        options = {};

    require('nodefly').profile(
      '00000000000000000000000000000000000000000', // <-- enter your nodefly dev key
      [ app_name,                                  // See http://nodefly.com/#howto 
        host_url,
        gear_id], // to identify multiple gears or processes (for scaled apps)
      options // optional
    );

Push these changes to your OpenShift app:

    git add package.json server.js
    git commit -m "updating my NodeFly dev key, adding realtime app monitoring"
    git push

That's it, you can checkout your application at:

    http://nodefly-$yournamespace.rhcloud.com
