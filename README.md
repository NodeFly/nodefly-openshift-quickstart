Nodefly on OpenShift
======================
This git repository helps you to setup Nodefly and to showcases a working configuration of the Nodefly agent.


Running on OpenShift
----------------------------

Create a Nodefly account at http://apm.nodefly.com/.

Create an account at http://openshift.redhat.com/ and set up you local machine with the client tools.

Create a node-0.6 application (you can call your application whatever you want) and change into the application directory.
<pre>
  rhc app create nodefly nodejs-0.6 --from-code https://github.com/NodeFly/nodefly-openshift-quickstart
  cd nodefly
</pre>

###Configuration###
Configure <strong>server.js</strong> file with your information:

<pre>
  require('nodefly').profile('app_key', 'app_name')
</pre>

Then push the repo
<pre>
  git add .
  git commit -m "my first commmit"
  git push
</pre>

That's it, you can now checkout your application at:
<pre>
  http://nodefly-$yournamespace.rhcloud.com
</pre>