# Virtual Machines

Suppose your customer installs your app on a virtual machine \(like VirtualBox, VMWare, Parallels, Xen, Microsoft Hyper-V, etc.\). With typical node locked licensing, on activation the fingerprint generated is of the virtual machine and not the host machine. Now, your customer can clone the instance of virtual machine running your app and run it again on every cloned virtual machine instance without paying for extra copies of your app \(because the cloned virtual machines are identical\). If you want to get paid for each copy of your product you definitely don't want to allow that.

## Disallowing VM Activations

You can allow or disallow VM activations at the product version level as well as product key level. Hence, you can disallow VM activations in general and at the same time allow it for few product keys if required.

### Disallowing VM Activations at Product Version Level

To disallow it at the product version level, you can uncheck the "Allow VM Activation" checkbox while creating the product or product version. If you have already created a product version, you can edit the same to change VM activation option.

![virtual-machines](https://cryptlex.com/public/img/docs/add-product.png)

The option to allow or disallow VM activation will automatically be inherited by all product keys.

### Disallowing VM Activations at Product Key Level

You can selectively allow or disallow VM activation for your product keys while creating or editing a product key. The default behaviour is inherited from the parent version of the product key. So, if you allowed VM activations at product version level the "Allow VM Activation" will automatically appear selected.

![virtual-machines](https://cryptlex.com/public/img/docs/add-pkey.png)

