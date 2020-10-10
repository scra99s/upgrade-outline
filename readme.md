# Overall Plan for Ubuntu20 upgrade

## Inital Package creation:
* Build all images required for swarm (within master-seed container)
* Create cloud-init .iso files for each node/vm (within master-seed container)
  * core will 3-4 node(vm)
  * core will be mixed swarm and "installed on VM" applications
  * sensor will be 6 nodes
  * sensor will be swarm only

## Package deployment:
* Deploy esxi, vcenter as per normal configuration (minor changes in networking) << this can be largely automated as I've proved before!!
* Each Node is deployed via Ubuntu20.OVA
* The cloud-init .iso is attached to its matching node and started.
  * builds and configures each underlying host.
  * loads all pre-built docker images into a local registry.
  * Creates a swarm and loads images from registry as services.
* Laptops deployed with a standard ubuntu20 server cloud-init image, meta-data and user-data is provided via PXE

## Notes
* Included code loosely outlines how the inital package creation will work.
* Code probably won't actually run as ive added sort of meta examples
* I have good plan for general system monitoring (daily check simplification) see prometheus
* Easier backups (centralised storage, atleast for swarm services)
* Far less complicated to produce the inital packages than before (therefore easier to sustain)
* Almost OS agnostic (so long as it has cloud init and the non-docker applications are compatible)
* Easier OS upgrades due to the above.
