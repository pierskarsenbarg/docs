
---
title: "BackendAddressPoolAddress"
title_tag: "azure.lb.BackendAddressPoolAddress"
meta_desc: "Documentation for the azure.lb.BackendAddressPoolAddress resource with examples, input properties, output properties, lookup functions, and supporting types."
---



<!-- WARNING: this file was generated by Pulumi Docs Generator. -->
<!-- Do not edit by hand unless you're certain you know what you are doing! -->

Manages a Backend Address within a Backend Address Pool.

> **Note:** Backend Addresses can only be added to a `Standard` SKU Load Balancer.

{{% examples %}}
## Example Usage

{{< chooser language "typescript,python,go,csharp" / >}}

{{% example csharp %}}
```csharp
using Pulumi;
using Azure = Pulumi.Azure;

class MyStack : Stack
{
    public MyStack()
    {
        var exampleVirtualNetwork = Output.Create(Azure.Network.GetVirtualNetwork.InvokeAsync(new Azure.Network.GetVirtualNetworkArgs
        {
            Name = "example-network",
            ResourceGroupName = "example-resources",
        }));
        var exampleLB = Output.Create(Azure.Lb.GetLB.InvokeAsync(new Azure.Lb.GetLBArgs
        {
            Name = "example-lb",
            ResourceGroupName = "example-resources",
        }));
        var exampleBackendAddressPool = exampleLB.Apply(exampleLB => Output.Create(Azure.Lb.GetBackendAddressPool.InvokeAsync(new Azure.Lb.GetBackendAddressPoolArgs
        {
            Name = "first",
            LoadbalancerId = exampleLB.Id,
        })));
        var exampleBackendAddressPoolAddress = new Azure.Lb.BackendAddressPoolAddress("exampleBackendAddressPoolAddress", new Azure.Lb.BackendAddressPoolAddressArgs
        {
            BackendAddressPoolId = exampleBackendAddressPool.Apply(exampleBackendAddressPool => exampleBackendAddressPool.Id),
            VirtualNetworkId = exampleVirtualNetwork.Apply(exampleVirtualNetwork => exampleVirtualNetwork.Id),
            IpAddress = "10.0.0.1",
        });
    }

}
```

{{% /example %}}

{{% example go %}}
```go
package main

import (
	"github.com/pulumi/pulumi-azure/sdk/v3/go/azure/lb"
	"github.com/pulumi/pulumi-azure/sdk/v3/go/azure/network"
	"github.com/pulumi/pulumi/sdk/v2/go/pulumi"
)

func main() {
	pulumi.Run(func(ctx *pulumi.Context) error {
		exampleVirtualNetwork, err := network.LookupVirtualNetwork(ctx, &network.LookupVirtualNetworkArgs{
			Name:              "example-network",
			ResourceGroupName: "example-resources",
		}, nil)
		if err != nil {
			return err
		}
		exampleLB, err := lb.GetLB(ctx, &lb.GetLBArgs{
			Name:              "example-lb",
			ResourceGroupName: "example-resources",
		}, nil)
		if err != nil {
			return err
		}
		exampleBackendAddressPool, err := lb.LookupBackendAddressPool(ctx, &lb.LookupBackendAddressPoolArgs{
			Name:           "first",
			LoadbalancerId: exampleLB.Id,
		}, nil)
		if err != nil {
			return err
		}
		_, err = lb.NewBackendAddressPoolAddress(ctx, "exampleBackendAddressPoolAddress", &lb.BackendAddressPoolAddressArgs{
			BackendAddressPoolId: pulumi.String(exampleBackendAddressPool.Id),
			VirtualNetworkId:     pulumi.String(exampleVirtualNetwork.Id),
			IpAddress:            pulumi.String("10.0.0.1"),
		})
		if err != nil {
			return err
		}
		return nil
	})
}
```

{{% /example %}}

{{% example python %}}
```python
import pulumi
import pulumi_azure as azure

example_virtual_network = azure.network.get_virtual_network(name="example-network",
    resource_group_name="example-resources")
example_lb = azure.lb.get_lb(name="example-lb",
    resource_group_name="example-resources")
example_backend_address_pool = azure.lb.get_backend_address_pool(name="first",
    loadbalancer_id=example_lb.id)
example_backend_address_pool_address = azure.lb.BackendAddressPoolAddress("exampleBackendAddressPoolAddress",
    backend_address_pool_id=example_backend_address_pool.id,
    virtual_network_id=example_virtual_network.id,
    ip_address="10.0.0.1")
```

{{% /example %}}

{{% example typescript %}}

```typescript
import * as pulumi from "@pulumi/pulumi";
import * as azure from "@pulumi/azure";

const exampleVirtualNetwork = azure.network.getVirtualNetwork({
    name: "example-network",
    resourceGroupName: "example-resources",
});
const exampleLB = azure.lb.getLB({
    name: "example-lb",
    resourceGroupName: "example-resources",
});
const exampleBackendAddressPool = exampleLB.then(exampleLB => azure.lb.getBackendAddressPool({
    name: "first",
    loadbalancerId: exampleLB.id,
}));
const exampleBackendAddressPoolAddress = new azure.lb.BackendAddressPoolAddress("exampleBackendAddressPoolAddress", {
    backendAddressPoolId: exampleBackendAddressPool.then(exampleBackendAddressPool => exampleBackendAddressPool.id),
    virtualNetworkId: exampleVirtualNetwork.then(exampleVirtualNetwork => exampleVirtualNetwork.id),
    ipAddress: "10.0.0.1",
});
```

{{% /example %}}

{{% /examples %}}


## Create a BackendAddressPoolAddress Resource {#create}
{{< chooser language "typescript,python,go,csharp" / >}}


{{% choosable language nodejs %}}
<div class="highlight"><pre class="chroma"><code class="language-typescript" data-lang="typescript"><span class="k">new </span><span class="nx">BackendAddressPoolAddress</span><span class="p">(</span><span class="nx">name</span><span class="p">:</span> <span class="nx">string</span><span class="p">, </span><span class="nx">args</span><span class="p">:</span> <span class="nx"><a href="#inputs">BackendAddressPoolAddressArgs</a></span><span class="p">, </span><span class="nx">opts</span><span class="p">?:</span> <span class="nx"><a href="/docs/reference/pkg/nodejs/pulumi/pulumi/#CustomResourceOptions">CustomResourceOptions</a></span><span class="p">);</span></code></pre></div>
{{% /choosable %}}

{{% choosable language python %}}
<div class="highlight"><pre class="chroma"><code class="language-python" data-lang="python"><span class="k">def </span><span class="nx">BackendAddressPoolAddress</span><span class="p">(</span><span class="nx">resource_name</span><span class="p">:</span> <span class="nx">str</span><span class="p">, </span><span class="nx">opts</span><span class="p">:</span> <span class="nx"><a href="/docs/reference/pkg/python/pulumi/#pulumi.ResourceOptions">Optional[ResourceOptions]</a></span> = None<span class="p">, </span><span class="nx">backend_address_pool_id</span><span class="p">:</span> <span class="nx">Optional[str]</span> = None<span class="p">, </span><span class="nx">ip_address</span><span class="p">:</span> <span class="nx">Optional[str]</span> = None<span class="p">, </span><span class="nx">name</span><span class="p">:</span> <span class="nx">Optional[str]</span> = None<span class="p">, </span><span class="nx">virtual_network_id</span><span class="p">:</span> <span class="nx">Optional[str]</span> = None<span class="p">)</span></code></pre></div>
{{% /choosable %}}

{{% choosable language go %}}
<div class="highlight"><pre class="chroma"><code class="language-go" data-lang="go"><span class="k">func </span><span class="nx">NewBackendAddressPoolAddress</span><span class="p">(</span><span class="nx">ctx</span><span class="p"> *</span><span class="nx"><a href="https://pkg.go.dev/github.com/pulumi/pulumi/sdk/v3/go/pulumi?tab=doc#Context">Context</a></span><span class="p">, </span><span class="nx">name</span><span class="p"> </span><span class="nx">string</span><span class="p">, </span><span class="nx">args</span><span class="p"> </span><span class="nx"><a href="#inputs">BackendAddressPoolAddressArgs</a></span><span class="p">, </span><span class="nx">opts</span><span class="p"> ...</span><span class="nx"><a href="https://pkg.go.dev/github.com/pulumi/pulumi/sdk/v3/go/pulumi?tab=doc#ResourceOption">ResourceOption</a></span><span class="p">) (*<span class="nx">BackendAddressPoolAddress</span>, error)</span></code></pre></div>
{{% /choosable %}}

{{% choosable language csharp %}}
<div class="highlight"><pre class="chroma"><code class="language-csharp" data-lang="csharp"><span class="k">public </span><span class="nx">BackendAddressPoolAddress</span><span class="p">(</span><span class="nx">string</span><span class="p"> </span><span class="nx">name<span class="p">, </span><span class="nx"><a href="#inputs">BackendAddressPoolAddressArgs</a></span><span class="p"> </span><span class="nx">args<span class="p">, </span><span class="nx"><a href="/docs/reference/pkg/dotnet/Pulumi/Pulumi.CustomResourceOptions.html">CustomResourceOptions</a></span><span class="p">? </span><span class="nx">opts = null<span class="p">)</span></code></pre></div>
{{% /choosable %}}

{{% choosable language nodejs %}}

<dl class="resources-properties">
  
    <dt
        class="property-required" title="Required">
        <span>name</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>
      The unique name of the resource.
    </dd>
  
    <dt
        class="property-required" title="Required">
        <span>args</span>
        <span class="property-indicator"></span>
        <span class="property-type"><a href="#inputs">BackendAddressPoolAddressArgs</a></span>
    </dt>
    <dd>
      The arguments to resource properties.
    </dd>
  
    <dt
        class="property-optional" title="Optional">
        <span>opts</span>
        <span class="property-indicator"></span>
        <span class="property-type"><a href="/docs/reference/pkg/nodejs/pulumi/pulumi/#CustomResourceOptions">CustomResourceOptions</a></span>
    </dt>
    <dd>
      Bag of options to control resource&#39;s behavior.
    </dd>
  

</dl>

{{% /choosable %}}

{{% choosable language python %}}

<dl class="resources-properties">
    <dt class="property-required" title="Required">
        <span>resource_name</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>The unique name of the resource.</dd>
    <dt class="property-optional" title="Optional">
        <span>opts</span>
        <span class="property-indicator"></span>
        <span class="property-type">
            <a href="/docs/reference/pkg/python/pulumi/#pulumi.ResourceOptions">ResourceOptions</a>
        </span>
    </dt>
    <dd>A bag of options that control this resource's behavior.</dd>
</dl>
{{% /choosable %}}

{{% choosable language go %}}

<dl class="resources-properties">
  
    <dt
        class="property-optional" title="Optional">
        <span>ctx</span>
        <span class="property-indicator"></span>
        <span class="property-type"><a href="https://pkg.go.dev/github.com/pulumi/pulumi/sdk/v3/go/pulumi?tab=doc#Context">Context</a></span>
    </dt>
    <dd>
      Context object for the current deployment.
    </dd>
  
    <dt
        class="property-required" title="Required">
        <span>name</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>
      The unique name of the resource.
    </dd>
  
    <dt
        class="property-required" title="Required">
        <span>args</span>
        <span class="property-indicator"></span>
        <span class="property-type"><a href="#inputs">BackendAddressPoolAddressArgs</a></span>
    </dt>
    <dd>
      The arguments to resource properties.
    </dd>
  
    <dt
        class="property-optional" title="Optional">
        <span>opts</span>
        <span class="property-indicator"></span>
        <span class="property-type"><a href="https://pkg.go.dev/github.com/pulumi/pulumi/sdk/v3/go/pulumi?tab=doc#ResourceOption">ResourceOption</a></span>
    </dt>
    <dd>
      Bag of options to control resource&#39;s behavior.
    </dd>
  

</dl>

{{% /choosable %}}

{{% choosable language csharp %}}

<dl class="resources-properties">
  
    <dt
        class="property-required" title="Required">
        <span>name</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>
      The unique name of the resource.
    </dd>
  
    <dt
        class="property-required" title="Required">
        <span>args</span>
        <span class="property-indicator"></span>
        <span class="property-type"><a href="#inputs">BackendAddressPoolAddressArgs</a></span>
    </dt>
    <dd>
      The arguments to resource properties.
    </dd>
  
    <dt
        class="property-optional" title="Optional">
        <span>opts</span>
        <span class="property-indicator"></span>
        <span class="property-type"><a href="/docs/reference/pkg/dotnet/Pulumi/Pulumi.CustomResourceOptions.html">CustomResourceOptions</a></span>
    </dt>
    <dd>
      Bag of options to control resource&#39;s behavior.
    </dd>
  

</dl>

{{% /choosable %}}

## BackendAddressPoolAddress Resource Properties {#properties}

To learn more about resource properties and how to use them, see [Inputs and Outputs]({{< relref "/docs/intro/concepts/inputs-outputs" >}}) in the Programming Model docs.

### Inputs

The BackendAddressPoolAddress resource accepts the following [input]({{< relref "/docs/intro/concepts/inputs-outputs" >}}) properties:



{{% choosable language csharp %}}
<dl class="resources-properties">

    <dt class="property-required"
            title="Required">
        <span id="backendaddresspoolid_csharp">
<a href="#backendaddresspoolid_csharp" style="color: inherit; text-decoration: inherit;">Backend<wbr>Address<wbr>Pool<wbr>Id</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The ID of the Backend Address Pool. Changing this forces a new Backend Address Pool Address to be created.
{{% /md %}}</dd>
    <dt class="property-required"
            title="Required">
        <span id="ipaddress_csharp">
<a href="#ipaddress_csharp" style="color: inherit; text-decoration: inherit;">Ip<wbr>Address</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The Static IP Address which should be allocated to this Backend Address Pool.
{{% /md %}}</dd>
    <dt class="property-required"
            title="Required">
        <span id="virtualnetworkid_csharp">
<a href="#virtualnetworkid_csharp" style="color: inherit; text-decoration: inherit;">Virtual<wbr>Network<wbr>Id</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The ID of the Virtual Network within which the Backend Address Pool should exist.
{{% /md %}}</dd>
    <dt class="property-optional"
            title="Optional">
        <span id="name_csharp">
<a href="#name_csharp" style="color: inherit; text-decoration: inherit;">Name</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The name which should be used for this Backend Address Pool Address. Changing this forces a new Backend Address Pool Address to be created.
{{% /md %}}</dd>
</dl>
{{% /choosable %}}

{{% choosable language go %}}
<dl class="resources-properties">

    <dt class="property-required"
            title="Required">
        <span id="backendaddresspoolid_go">
<a href="#backendaddresspoolid_go" style="color: inherit; text-decoration: inherit;">Backend<wbr>Address<wbr>Pool<wbr>Id</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The ID of the Backend Address Pool. Changing this forces a new Backend Address Pool Address to be created.
{{% /md %}}</dd>
    <dt class="property-required"
            title="Required">
        <span id="ipaddress_go">
<a href="#ipaddress_go" style="color: inherit; text-decoration: inherit;">Ip<wbr>Address</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The Static IP Address which should be allocated to this Backend Address Pool.
{{% /md %}}</dd>
    <dt class="property-required"
            title="Required">
        <span id="virtualnetworkid_go">
<a href="#virtualnetworkid_go" style="color: inherit; text-decoration: inherit;">Virtual<wbr>Network<wbr>Id</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The ID of the Virtual Network within which the Backend Address Pool should exist.
{{% /md %}}</dd>
    <dt class="property-optional"
            title="Optional">
        <span id="name_go">
<a href="#name_go" style="color: inherit; text-decoration: inherit;">Name</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The name which should be used for this Backend Address Pool Address. Changing this forces a new Backend Address Pool Address to be created.
{{% /md %}}</dd>
</dl>
{{% /choosable %}}

{{% choosable language nodejs %}}
<dl class="resources-properties">

    <dt class="property-required"
            title="Required">
        <span id="backendaddresspoolid_nodejs">
<a href="#backendaddresspoolid_nodejs" style="color: inherit; text-decoration: inherit;">backend<wbr>Address<wbr>Pool<wbr>Id</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The ID of the Backend Address Pool. Changing this forces a new Backend Address Pool Address to be created.
{{% /md %}}</dd>
    <dt class="property-required"
            title="Required">
        <span id="ipaddress_nodejs">
<a href="#ipaddress_nodejs" style="color: inherit; text-decoration: inherit;">ip<wbr>Address</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The Static IP Address which should be allocated to this Backend Address Pool.
{{% /md %}}</dd>
    <dt class="property-required"
            title="Required">
        <span id="virtualnetworkid_nodejs">
<a href="#virtualnetworkid_nodejs" style="color: inherit; text-decoration: inherit;">virtual<wbr>Network<wbr>Id</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The ID of the Virtual Network within which the Backend Address Pool should exist.
{{% /md %}}</dd>
    <dt class="property-optional"
            title="Optional">
        <span id="name_nodejs">
<a href="#name_nodejs" style="color: inherit; text-decoration: inherit;">name</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The name which should be used for this Backend Address Pool Address. Changing this forces a new Backend Address Pool Address to be created.
{{% /md %}}</dd>
</dl>
{{% /choosable %}}

{{% choosable language python %}}
<dl class="resources-properties">

    <dt class="property-required"
            title="Required">
        <span id="backend_address_pool_id_python">
<a href="#backend_address_pool_id_python" style="color: inherit; text-decoration: inherit;">backend_<wbr>address_<wbr>pool_<wbr>id</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}The ID of the Backend Address Pool. Changing this forces a new Backend Address Pool Address to be created.
{{% /md %}}</dd>
    <dt class="property-required"
            title="Required">
        <span id="ip_address_python">
<a href="#ip_address_python" style="color: inherit; text-decoration: inherit;">ip_<wbr>address</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}The Static IP Address which should be allocated to this Backend Address Pool.
{{% /md %}}</dd>
    <dt class="property-required"
            title="Required">
        <span id="virtual_network_id_python">
<a href="#virtual_network_id_python" style="color: inherit; text-decoration: inherit;">virtual_<wbr>network_<wbr>id</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}The ID of the Virtual Network within which the Backend Address Pool should exist.
{{% /md %}}</dd>
    <dt class="property-optional"
            title="Optional">
        <span id="name_python">
<a href="#name_python" style="color: inherit; text-decoration: inherit;">name</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}The name which should be used for this Backend Address Pool Address. Changing this forces a new Backend Address Pool Address to be created.
{{% /md %}}</dd>
</dl>
{{% /choosable %}}


### Outputs

All [input](#inputs) properties are implicitly available as output properties. Additionally, the BackendAddressPoolAddress resource produces the following output properties:



{{% choosable language csharp %}}
<dl class="resources-properties">

    <dt class="property-"
            title="">
        <span id="id_csharp">
<a href="#id_csharp" style="color: inherit; text-decoration: inherit;">Id</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The provider-assigned unique ID for this managed resource.{{% /md %}}</dd>
</dl>
{{% /choosable %}}

{{% choosable language go %}}
<dl class="resources-properties">

    <dt class="property-"
            title="">
        <span id="id_go">
<a href="#id_go" style="color: inherit; text-decoration: inherit;">Id</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The provider-assigned unique ID for this managed resource.{{% /md %}}</dd>
</dl>
{{% /choosable %}}

{{% choosable language nodejs %}}
<dl class="resources-properties">

    <dt class="property-"
            title="">
        <span id="id_nodejs">
<a href="#id_nodejs" style="color: inherit; text-decoration: inherit;">id</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The provider-assigned unique ID for this managed resource.{{% /md %}}</dd>
</dl>
{{% /choosable %}}

{{% choosable language python %}}
<dl class="resources-properties">

    <dt class="property-"
            title="">
        <span id="id_python">
<a href="#id_python" style="color: inherit; text-decoration: inherit;">id</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}The provider-assigned unique ID for this managed resource.{{% /md %}}</dd>
</dl>
{{% /choosable %}}



## Look up an Existing BackendAddressPoolAddress Resource {#look-up}

Get an existing BackendAddressPoolAddress resource's state with the given name, ID, and optional extra properties used to qualify the lookup.
{{< chooser language "typescript,python,go,csharp" / >}}

{{% choosable language nodejs %}}
<div class="highlight"><pre class="chroma"><code class="language-typescript" data-lang="typescript"><span class="k">public static </span><span class="nf">get</span><span class="p">(</span><span class="nx">name</span><span class="p">:</span> <span class="nx">string</span><span class="p">, </span><span class="nx">id</span><span class="p">:</span> <span class="nx"><a href="/docs/reference/pkg/nodejs/pulumi/pulumi/#ID">Input&lt;ID&gt;</a></span><span class="p">, </span><span class="nx">state</span><span class="p">?:</span> <span class="nx">BackendAddressPoolAddressState</span><span class="p">, </span><span class="nx">opts</span><span class="p">?:</span> <span class="nx"><a href="/docs/reference/pkg/nodejs/pulumi/pulumi/#CustomResourceOptions">CustomResourceOptions</a></span><span class="p">): </span><span class="nx">BackendAddressPoolAddress</span></code></pre></div>
{{% /choosable %}}

{{% choosable language python %}}
<div class="highlight"><pre class="chroma"><code class="language-python" data-lang="python"><span class=nd>@staticmethod</span>
<span class="k">def </span><span class="nf">get</span><span class="p">(</span><span class="nx">resource_name</span><span class="p">:</span> <span class="nx">str</span><span class="p">, </span><span class="nx">id</span><span class="p">:</span> <span class="nx">str</span><span class="p">, </span><span class="nx">opts</span><span class="p">:</span> <span class="nx"><a href="/docs/reference/pkg/python/pulumi/#pulumi.ResourceOptions">Optional[ResourceOptions]</a></span> = None<span class="p">, </span><span class="nx">backend_address_pool_id</span><span class="p">:</span> <span class="nx">Optional[str]</span> = None<span class="p">, </span><span class="nx">ip_address</span><span class="p">:</span> <span class="nx">Optional[str]</span> = None<span class="p">, </span><span class="nx">name</span><span class="p">:</span> <span class="nx">Optional[str]</span> = None<span class="p">, </span><span class="nx">virtual_network_id</span><span class="p">:</span> <span class="nx">Optional[str]</span> = None<span class="p">) -&gt;</span> BackendAddressPoolAddress</code></pre></div>
{{% /choosable %}}

{{% choosable language go %}}
<div class="highlight"><pre class="chroma"><code class="language-go" data-lang="go"><span class="k">func </span>GetBackendAddressPoolAddress<span class="p">(</span><span class="nx">ctx</span><span class="p"> *</span><span class="nx"><a href="https://pkg.go.dev/github.com/pulumi/pulumi/sdk/v3/go/pulumi?tab=doc#Context">Context</a></span><span class="p">, </span><span class="nx">name</span><span class="p"> </span><span class="nx">string</span><span class="p">, </span><span class="nx">id</span><span class="p"> </span><span class="nx"><a href="https://pkg.go.dev/github.com/pulumi/pulumi/sdk/v3/go/pulumi?tab=doc#IDInput">IDInput</a></span><span class="p">, </span><span class="nx">state</span><span class="p"> *</span><span class="nx">BackendAddressPoolAddressState</span><span class="p">, </span><span class="nx">opts</span><span class="p"> ...</span><span class="nx"><a href="https://pkg.go.dev/github.com/pulumi/pulumi/sdk/v3/go/pulumi?tab=doc#ResourceOption">ResourceOption</a></span><span class="p">) (*<span class="nx">BackendAddressPoolAddress</span>, error)</span></code></pre></div>
{{% /choosable %}}

{{% choosable language csharp %}}
<div class="highlight"><pre class="chroma"><code class="language-csharp" data-lang="csharp"><span class="k">public static </span><span class="nx">BackendAddressPoolAddress</span><span class="nf"> Get</span><span class="p">(</span><span class="nx">string</span><span class="p"> </span><span class="nx">name<span class="p">, </span><span class="nx"><a href="/docs/reference/pkg/dotnet/Pulumi/Pulumi.Input-1.html">Input&lt;string&gt;</a></span><span class="p"> </span><span class="nx">id<span class="p">, </span><span class="nx">BackendAddressPoolAddressState</span><span class="p">? </span><span class="nx">state<span class="p">, </span><span class="nx"><a href="/docs/reference/pkg/dotnet/Pulumi/Pulumi.CustomResourceOptions.html">CustomResourceOptions</a></span><span class="p">? </span><span class="nx">opts = null<span class="p">)</span></code></pre></div>
{{% /choosable %}}

{{% choosable language nodejs %}}

<dl class="resources-properties">
    <dt class="property-required" title="Required">
        <span>name</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>The unique name of the resulting resource.</dd>
    <dt class="property-required" title="Required">
        <span>id</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>The <em>unique</em> provider ID of the resource to lookup.</dd>
    <dt class="property-optional" title="Optional">
        <span>state</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>Any extra arguments used during the lookup.</dd>
    <dt class="property-optional" title="Optional">
        <span>opts</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>A bag of options that control this resource's behavior.</dd>
</dl>

{{% /choosable %}}

{{% choosable language python %}}
<dl class="resources-properties">
    <dt class="property-required" title="Required">
        <span>resource_name</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>The unique name of the resulting resource.</dd>
    <dt class="property-required" title="Optional">
        <span>id</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>The <em>unique</em> provider ID of the resource to lookup.</dd>
</dl>
{{% /choosable %}}

{{% choosable language go %}}

<dl class="resources-properties">
    <dt class="property-required" title="Required">
        <span>name</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>The unique name of the resulting resource.</dd>
    <dt class="property-required" title="Required">
        <span>id</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>The <em>unique</em> provider ID of the resource to lookup.</dd>
    <dt class="property-optional" title="Optional">
        <span>state</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>Any extra arguments used during the lookup.</dd>
    <dt class="property-optional" title="Optional">
        <span>opts</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>A bag of options that control this resource's behavior.</dd>
</dl>

{{% /choosable %}}

{{% choosable language csharp %}}

<dl class="resources-properties">
    <dt class="property-required" title="Required">
        <span>name</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>The unique name of the resulting resource.</dd>
    <dt class="property-required" title="Required">
        <span>id</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>The <em>unique</em> provider ID of the resource to lookup.</dd>
    <dt class="property-optional" title="Optional">
        <span>state</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>Any extra arguments used during the lookup.</dd>
    <dt class="property-optional" title="Optional">
        <span>opts</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>A bag of options that control this resource's behavior.</dd>
</dl>

{{% /choosable %}}

The following state arguments are supported:


{{% choosable language csharp %}}
<dl class="resources-properties">

    <dt class="property-optional"
            title="Optional">
        <span id="state_backendaddresspoolid_csharp">
<a href="#state_backendaddresspoolid_csharp" style="color: inherit; text-decoration: inherit;">Backend<wbr>Address<wbr>Pool<wbr>Id</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The ID of the Backend Address Pool. Changing this forces a new Backend Address Pool Address to be created.
{{% /md %}}</dd>
    <dt class="property-optional"
            title="Optional">
        <span id="state_ipaddress_csharp">
<a href="#state_ipaddress_csharp" style="color: inherit; text-decoration: inherit;">Ip<wbr>Address</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The Static IP Address which should be allocated to this Backend Address Pool.
{{% /md %}}</dd>
    <dt class="property-optional"
            title="Optional">
        <span id="state_name_csharp">
<a href="#state_name_csharp" style="color: inherit; text-decoration: inherit;">Name</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The name which should be used for this Backend Address Pool Address. Changing this forces a new Backend Address Pool Address to be created.
{{% /md %}}</dd>
    <dt class="property-optional"
            title="Optional">
        <span id="state_virtualnetworkid_csharp">
<a href="#state_virtualnetworkid_csharp" style="color: inherit; text-decoration: inherit;">Virtual<wbr>Network<wbr>Id</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The ID of the Virtual Network within which the Backend Address Pool should exist.
{{% /md %}}</dd>
</dl>
{{% /choosable %}}

{{% choosable language go %}}
<dl class="resources-properties">

    <dt class="property-optional"
            title="Optional">
        <span id="state_backendaddresspoolid_go">
<a href="#state_backendaddresspoolid_go" style="color: inherit; text-decoration: inherit;">Backend<wbr>Address<wbr>Pool<wbr>Id</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The ID of the Backend Address Pool. Changing this forces a new Backend Address Pool Address to be created.
{{% /md %}}</dd>
    <dt class="property-optional"
            title="Optional">
        <span id="state_ipaddress_go">
<a href="#state_ipaddress_go" style="color: inherit; text-decoration: inherit;">Ip<wbr>Address</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The Static IP Address which should be allocated to this Backend Address Pool.
{{% /md %}}</dd>
    <dt class="property-optional"
            title="Optional">
        <span id="state_name_go">
<a href="#state_name_go" style="color: inherit; text-decoration: inherit;">Name</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The name which should be used for this Backend Address Pool Address. Changing this forces a new Backend Address Pool Address to be created.
{{% /md %}}</dd>
    <dt class="property-optional"
            title="Optional">
        <span id="state_virtualnetworkid_go">
<a href="#state_virtualnetworkid_go" style="color: inherit; text-decoration: inherit;">Virtual<wbr>Network<wbr>Id</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The ID of the Virtual Network within which the Backend Address Pool should exist.
{{% /md %}}</dd>
</dl>
{{% /choosable %}}

{{% choosable language nodejs %}}
<dl class="resources-properties">

    <dt class="property-optional"
            title="Optional">
        <span id="state_backendaddresspoolid_nodejs">
<a href="#state_backendaddresspoolid_nodejs" style="color: inherit; text-decoration: inherit;">backend<wbr>Address<wbr>Pool<wbr>Id</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The ID of the Backend Address Pool. Changing this forces a new Backend Address Pool Address to be created.
{{% /md %}}</dd>
    <dt class="property-optional"
            title="Optional">
        <span id="state_ipaddress_nodejs">
<a href="#state_ipaddress_nodejs" style="color: inherit; text-decoration: inherit;">ip<wbr>Address</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The Static IP Address which should be allocated to this Backend Address Pool.
{{% /md %}}</dd>
    <dt class="property-optional"
            title="Optional">
        <span id="state_name_nodejs">
<a href="#state_name_nodejs" style="color: inherit; text-decoration: inherit;">name</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The name which should be used for this Backend Address Pool Address. Changing this forces a new Backend Address Pool Address to be created.
{{% /md %}}</dd>
    <dt class="property-optional"
            title="Optional">
        <span id="state_virtualnetworkid_nodejs">
<a href="#state_virtualnetworkid_nodejs" style="color: inherit; text-decoration: inherit;">virtual<wbr>Network<wbr>Id</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The ID of the Virtual Network within which the Backend Address Pool should exist.
{{% /md %}}</dd>
</dl>
{{% /choosable %}}

{{% choosable language python %}}
<dl class="resources-properties">

    <dt class="property-optional"
            title="Optional">
        <span id="state_backend_address_pool_id_python">
<a href="#state_backend_address_pool_id_python" style="color: inherit; text-decoration: inherit;">backend_<wbr>address_<wbr>pool_<wbr>id</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}The ID of the Backend Address Pool. Changing this forces a new Backend Address Pool Address to be created.
{{% /md %}}</dd>
    <dt class="property-optional"
            title="Optional">
        <span id="state_ip_address_python">
<a href="#state_ip_address_python" style="color: inherit; text-decoration: inherit;">ip_<wbr>address</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}The Static IP Address which should be allocated to this Backend Address Pool.
{{% /md %}}</dd>
    <dt class="property-optional"
            title="Optional">
        <span id="state_name_python">
<a href="#state_name_python" style="color: inherit; text-decoration: inherit;">name</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}The name which should be used for this Backend Address Pool Address. Changing this forces a new Backend Address Pool Address to be created.
{{% /md %}}</dd>
    <dt class="property-optional"
            title="Optional">
        <span id="state_virtual_network_id_python">
<a href="#state_virtual_network_id_python" style="color: inherit; text-decoration: inherit;">virtual_<wbr>network_<wbr>id</a>
</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}The ID of the Virtual Network within which the Backend Address Pool should exist.
{{% /md %}}</dd>
</dl>
{{% /choosable %}}





## Import


Backend Address Pool Addresses can be imported using the `resource id`, e.g.

```sh
 $ pulumi import azure:lb/backendAddressPoolAddress:BackendAddressPoolAddress example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/group1/providers/Microsoft.Network/loadBalancers/loadBalancer1/backendAddressPools/backendAddressPool1/addresses/address1
```




<h2 id="package-details">Package Details</h2>
<dl class="package-details">
	<dt>Repository</dt>
	<dd><a href="https://github.com/pulumi/pulumi-azure">https://github.com/pulumi/pulumi-azure</a></dd>
	<dt>License</dt>
	<dd>Apache-2.0</dd>
	<dt>Notes</dt>
	<dd>This Pulumi package is based on the [`azurerm` Terraform Provider](https://github.com/terraform-providers/terraform-provider-azurerm).</dd>
</dl>
