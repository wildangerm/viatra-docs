The EMF-IncQuery [Viewers Framework](https://wiki.eclipse.org/EMFIncQuery/UserDocumentation/IncQuery_Viewers) is applied to create custom views for the CPS demonstrator.

The views are defined using declarative pattern annotations which specify items and edges in a view. The view may be a graph visualization, but simple UI elements, such as lists or tree views are also supported by the technology. In the CPS demonstrator, we created views using the [Zest](https://www.eclipse.org/gef/zest/) Graph Visualization framework.

![Deployment model viewer](https://raw.githubusercontent.com/IncQueryLabs/incquery-examples-cps/master/models/org.eclipse.incquery.examples.cps.instances/deployment_viewer.png)

The definition of the views can be found in the `cps.queries` project in the `model/viewer` and `deployment/viewer` packages. Items are defined with `@Item` annotations, edges are specified with `@Edge` annotations, while the format (such as colours) is described with `@Format` annotations.

## Viewer example

The following patterns define the following:
* Create items for each deployment host
* Create items for each deployment application
* Create edges between items that correspond to the deployment host and application objects

```
@Format(color = "#FBFE00")
@Item(item = host, label = "Host $host.ip$")
pattern deploymentHostItem(host) {
	DeploymentHost(host);
}

@Format(color = "#996600")
@Item(item = app, label = "App $app.id$")
pattern deploymentApplicationItem(app) {
	DeploymentApplication(app);
}

@Edge(source = host, target = app, label = "apps")
pattern deploymentHostApplicationEdge(host, app) {
	DeploymentHost.applications(host, app);
}
```