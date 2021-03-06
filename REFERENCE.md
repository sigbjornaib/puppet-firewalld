# Reference
<!-- DO NOT EDIT: This document was generated by Puppet Strings -->

## Table of Contents

**Classes**

* [`firewalld`](#firewalld): == Class: firewalld  Manage the firewalld service  See the README.md for usage instructions for the firewalld_zone and firewalld_rich_rule ty

**Defined types**

* [`firewalld::custom_service`](#firewalldcustom_service): == Type: firewalld::custom_service  Creates a new service definition for use in firewalld  See the README.md for usage instructions for this 

**Resource types**

* [`firewalld_direct_chain`](#firewalld_direct_chain): Allow to create a custom chain in iptables/ip6tables/ebtables using firewalld direct interface.  Example:      firewalld_direct_chain {'Add c
* [`firewalld_direct_passthrough`](#firewalld_direct_passthrough): Allow to create a custom passthroughhrough traffic in iptables/ip6tables/ebtables using firewalld direct interface.  Example:      firewalld_
* [`firewalld_direct_purge`](#firewalld_direct_purge): Allow to purge direct rules in iptables/ip6tables/ebtables using firewalld direct interface.  Example:      firewalld_direct_purge {'chain': 
* [`firewalld_direct_rule`](#firewalld_direct_rule): Allow to pass rules directly to iptables/ip6tables/ebtables using firewalld direct interface.  Example:      firewalld_direct_rule {'Allow ou
* [`firewalld_ipset`](#firewalld_ipset): Configure IPsets in Firewalld  Example:     firewalld_ipset {'internal net':         ensure   => 'present',         type     => 'hash:net',  
* [`firewalld_port`](#firewalld_port): Assigns a port to a specific firewalld zone. firewalld_port will autorequire the firewalld_zone specified in the zone parameter so there is n
* [`firewalld_rich_rule`](#firewalld_rich_rule): Manages firewalld rich rules.  firewalld_rich_rules will autorequire the firewalld_zone specified in the zone parameter so there is no need t
* [`firewalld_service`](#firewalld_service): Assigns a service to a specific firewalld zone.
* [`firewalld_zone`](#firewalld_zone): Creates and manages firewalld zones.

## Classes

### firewalld

== Class: firewalld

Manage the firewalld service

See the README.md for usage instructions for the firewalld_zone and
firewalld_rich_rule types

=== Examples

 Standard:
   include firewalld

 Command line only, no GUI components:
   class{'firewalld':
   }

 With GUI components
   class{'firewalld':
     install_gui => true,
   }



=== Authors

Craig Dunn <craig@craigdunn.org>

=== Copyright

Copyright 2015 Craig Dunn

#### Parameters

The following parameters are available in the `firewalld` class.

##### `package_ensure`

Data type: `Enum['present','absent','latest','installed']`



Default value: 'installed'

##### `package`

Data type: `String`



Default value: 'firewalld'

##### `service_ensure`

Data type: `Stdlib::Ensure::Service`



Default value: 'running'

##### `config_package`

Data type: `String`



Default value: 'firewall-config'

##### `install_gui`

Data type: `Boolean`



Default value: `false`

##### `service_enable`

Data type: `Boolean`



Default value: `true`

##### `zones`

Data type: `Hash`



Default value: {}

##### `ports`

Data type: `Hash`



Default value: {}

##### `services`

Data type: `Hash`



Default value: {}

##### `rich_rules`

Data type: `Hash`



Default value: {}

##### `custom_services`

Data type: `Hash`



Default value: {}

##### `ipsets`

Data type: `Hash`



Default value: {}

##### `direct_rules`

Data type: `Hash`



Default value: {}

##### `direct_chains`

Data type: `Hash`



Default value: {}

##### `direct_passthroughs`

Data type: `Hash`



Default value: {}

##### `purge_direct_rules`

Data type: `Boolean`



Default value: `false`

##### `purge_direct_chains`

Data type: `Boolean`



Default value: `false`

##### `purge_direct_passthroughs`

Data type: `Boolean`



Default value: `false`

##### `purge_unknown_ipsets`

Data type: `Boolean`



Default value: `false`

##### `default_zone`

Data type: `Optional[String]`



Default value: `undef`

##### `log_denied`

Data type: `Optional[Enum['off','all','unicast','broadcast','multicast']]`



Default value: `undef`

##### `cleanup_on_exit`

Data type: `Optional[Enum['yes', 'no']]`



Default value: `undef`

##### `minimal_mark`

Data type: `Optional[Integer]`



Default value: `undef`

##### `lockdown`

Data type: `Optional[Enum['yes', 'no']]`



Default value: `undef`

##### `ipv6_rpfilter`

Data type: `Optional[Enum['yes', 'no']]`



Default value: `undef`

##### `firewall_backend`

Data type: `Optional[Enum['iptables', 'nftables']]`



Default value: `undef`

##### `default_service_zone`

Data type: `Optional[String]`



Default value: `undef`

##### `default_port_zone`

Data type: `Optional[String]`



Default value: `undef`

##### `default_port_protocol`

Data type: `Optional[String]`



Default value: `undef`

## Defined types

### firewalld::custom_service

== Type: firewalld::custom_service

Creates a new service definition for use in firewalld

See the README.md for usage instructions for this defined type

=== Examples

   firewalld::custom_service{'My Custom Service':
     short       => 'MyService',
     description => 'My Custom Service is a daemon that does whatever',
     port        => [
       {
           'port'     => '1234'
           'protocol' => 'tcp'
       },
       {
           'port'     => '1234'
           'protocol' => 'udp'
       },
     ],
     module      => ['nf_conntrack_netbios_ns'],
     destination => {
       'ipv4' => '127.0.0.1',
       'ipv6' => '::1'
     }
   }

=== Authors

Andrew Patik <andrewpatik@gmail.com>

#### Parameters

The following parameters are available in the `firewalld::custom_service` defined type.

##### `short`

Data type: `String`



Default value: $name

##### `description`

Data type: `Optional[String]`



Default value: `undef`

##### `port`

Data type: `Optional[Array[Hash]]`



Default value: `undef`

##### `module`

Data type: `Optional[Array[String]]`



Default value: `undef`

##### `destination`

Data type: `Optional[Hash[
    Enum['ipv4', 'ipv6'],
    String
  ]]`



Default value: `undef`

##### `filename`

Data type: `String`



Default value: $short

##### `config_dir`

Data type: `Stdlib::Unixpath`



Default value: '/etc/firewalld/services'

##### `ensure`

Data type: `Enum['present','absent']`



Default value: 'present'

## Resource types

### firewalld_direct_chain

Allow to create a custom chain in iptables/ip6tables/ebtables using firewalld direct interface.

Example:

    firewalld_direct_chain {'Add custom chain LOG_DROPS':
        name           => 'LOG_DROPS',
        ensure         => 'present',
        inet_protocol  => 'ipv4',
        table          => 'filter'
    }

#### Properties

The following properties are available in the `firewalld_direct_chain` type.

##### `ensure`

Valid values: present, absent

The basic property that the resource should be in.

Default value: present

#### Parameters

The following parameters are available in the `firewalld_direct_chain` type.

##### `name`

Name of the chain eg: LOG_DROPS

##### `inet_protocol`

Valid values: ipv4, ipv6

namevar

Name of the TCP/IP protocol to use (e.g: ipv4, ipv6)

Default value: ipv4

##### `table`

namevar

Name of the table type to add (e.g: filter, nat, mangle, raw)

### firewalld_direct_passthrough

Allow to create a custom passthroughhrough traffic in iptables/ip6tables/ebtables using firewalld direct interface.

Example:

    firewalld_direct_passthrough {'Forward traffic from OUTPUT to OUTPUT_filter':
        ensure        => 'present',
        inet_protocol => 'ipv4',
        args          => '-A OUTPUT -j OUTPUT_filter',
    }

Or using namevar

    firewalld_direct_passthrough {'-A OUTPUT -j OUTPUT_filter':
        ensure        => 'present',
    }

#### Properties

The following properties are available in the `firewalld_direct_passthrough` type.

##### `ensure`

Valid values: present, absent

The basic property that the resource should be in.

Default value: present

#### Parameters

The following parameters are available in the `firewalld_direct_passthrough` type.

##### `inet_protocol`

Valid values: ipv4, ipv6

Name of the TCP/IP protocol to use (e.g: ipv4, ipv6)

Default value: ipv4

##### `args`

namevar

Name of the passthroughhrough to add (e.g: -A OUTPUT -j OUTPUT_filter)

### firewalld_direct_purge

Allow to purge direct rules in iptables/ip6tables/ebtables using firewalld direct interface.

Example:

    firewalld_direct_purge {'chain': }
    firewalld_direct_purge {'passthrough': }
    firewalld_direct_purge {'rule': }

#### Properties

The following properties are available in the `firewalld_direct_purge` type.

##### `ensure`

Valid values: purgable, purged

The basic property that the resource should be in.

Default value: purged

#### Parameters

The following parameters are available in the `firewalld_direct_purge` type.

##### `purge`

Valid values: `true`, `false`



Default value: `true`

##### `name`

Valid values: chain, passthrough, rule

namevar

Type of resource to purge, valid values are 'chain', 'passthrough' and 'rule'

### firewalld_direct_rule

Allow to pass rules directly to iptables/ip6tables/ebtables using firewalld direct interface.

Example:

    firewalld_direct_rule {'Allow outgoing SSH connection':
        ensure         => 'present',
        inet_protocol  => 'ipv4',
        table          => 'filter',
        chain          => 'OUTPUT',
        priority       => 1,
        args           => '-p tcp --dport=22 -j ACCEPT',
    }

#### Properties

The following properties are available in the `firewalld_direct_rule` type.

##### `ensure`

Valid values: present, absent

The basic property that the resource should be in.

Default value: present

#### Parameters

The following parameters are available in the `firewalld_direct_rule` type.

##### `name`

namevar

Name of the rule resource in Puppet

##### `inet_protocol`

Valid values: ipv4, ipv6

Name of the TCP/IP protocol to use (e.g: ipv4, ipv6)

Default value: ipv4

##### `table`

Name of the table type to add (e.g: filter, nat, mangle, raw)

##### `chain`

Name of the chain type to add (e.g: INPUT, OUTPUT, FORWARD)

##### `priority`

The priority number of the rule (e.g: 0, 1, 2, ... 99)

##### `args`

<args> can be all iptables, ip6tables and ebtables command line arguments

### firewalld_ipset

Configure IPsets in Firewalld

Example:
    firewalld_ipset {'internal net':
        ensure   => 'present',
        type     => 'hash:net',
        family   => 'inet',
        entries  => ['192.168.0.0/24']
    }

#### Properties

The following properties are available in the `firewalld_ipset` type.

##### `ensure`

Valid values: present, absent

The basic property that the resource should be in.

Default value: present

##### `entries`

Array of ipset entries

##### `family`

Valid values: inet6, inet

Protocol family of the IPSet

##### `hashsize`

Initial hash size of the IPSet

##### `maxelem`

Valid values: %r{^[1-9]\d*$}

Maximal number of elements that can be stored in the set

##### `timeout`

Valid values: %r{^\d+$}

Timeout in seconds before entries expiry. 0 means entry is permanent

#### Parameters

The following parameters are available in the `firewalld_ipset` type.

##### `name`

namevar

Name of the IPset

##### `type`

Valid values: bitmap:ip, bitmap:ip,mac, bitmap:port, hash:ip, hash:ip,mark, hash:ip,port, hash:ip,port,ip, hash:ip,port,net, hash:mac, hash:net, hash:net,iface, hash:net,net, hash:net,port, hash:net,port,net, list:set

Type of the ipset (default: hash:ip)

Default value: hash:ip

##### `options`

Hash of options for the IPset, eg { 'family' => 'inet6' }

##### `manage_entries`

Valid values: `true`, `false`, yes, no

Should we manage entries in this ipset or leave another process manage those entries

Default value: `true`

### firewalld_port

Assigns a port to a specific firewalld zone.
firewalld_port will autorequire the firewalld_zone specified in the zone parameter so there is no need to add dependencies for this

Example:

    firewalld_port {'Open port 8080 in the public Zone':
        ensure   => 'present',
        zone     => 'public',
        port     => 8080,
        protocol => 'tcp',
    }

#### Properties

The following properties are available in the `firewalld_port` type.

##### `ensure`

Valid values: present, absent

The basic property that the resource should be in.

Default value: present

#### Parameters

The following parameters are available in the `firewalld_port` type.

##### `name`

namevar

Name of the port resource in Puppet

##### `zone`

Name of the zone to which you want to add the port

##### `port`

Specify the element as a port

##### `protocol`

Specify the element as a protocol

### firewalld_rich_rule

Manages firewalld rich rules.

firewalld_rich_rules will autorequire the firewalld_zone specified in the zone parameter so there is no need to add dependencies for this

Example:

  firewalld_rich_rule { 'Accept SSH from barny':
    ensure => present,
    zone   => 'restricted',
    source => '192.168.1.2/32',
    service => 'ssh',
    action  => 'accept',
  }

#### Properties

The following properties are available in the `firewalld_rich_rule` type.

##### `ensure`

Valid values: present, absent

The basic property that the resource should be in.

Default value: present

#### Parameters

The following parameters are available in the `firewalld_rich_rule` type.

##### `name`

namevar

Name of the rule resource in Puppet

##### `zone`

Name of the zone

##### `family`

Valid values: ipv4, ipv6

IP family, one of ipv4 or ipv6, defauts to ipv4

Default value: ipv4

##### `source`

Specify source address, this can be a string of the IP address or a hash containing other options

##### `dest`

Specify destination address, this can be a string of the IP address or a hash containing other options

##### `service`

Specify the element as a service

##### `port`

Specify the element as a port

##### `protocol`

Specify the element as a protocol

##### `icmp_block`

Specify the element as an icmp-block

##### `masquerade`

Specify the element as masquerade

##### `forward_port`

Specify the element as forward-port

##### `log`

doc

##### `audit`

doc

##### `action`



##### `raw_rule`

Manage the entire rule as one string - this is used internally by firwalld_zone to
handle pruning of rules

### firewalld_service

Assigns a service to a specific firewalld zone.

`firewalld_service` will autorequire the `firewalld_zone` specified in the
`zone` parameter and the `firewalld::custom_service` specified in the `service`
parameter. There is no need to manually add dependencies for this.

#### Examples

##### Allowing SSH

```puppet
firewalld_service {'Allow SSH in the public Zone':
    ensure  => present,
    zone    => 'public',
    service => 'ssh',
}
```

#### Properties

The following properties are available in the `firewalld_service` type.

##### `ensure`

Valid values: present, absent

The basic property that the resource should be in.

Default value: present

#### Parameters

The following parameters are available in the `firewalld_service` type.

##### `name`

namevar

Name of the service resource in Puppet

##### `service`

Name of the service to add

##### `zone`

Name of the zone to which you want to add the service

### firewalld_zone

Creates and manages firewalld zones.

Note that setting `ensure => 'absent'` to the built in firewalld zones will
not work, and will generate an error. This is a limitation of firewalld itself, not the module.

#### Examples

##### Create a zone called `restricted`

```puppet
firewalld_zone { 'restricted':
  ensure           => present,
  target           => '%%REJECT%%',
  interfaces       => [],
  sources          => [],
  purge_rich_rules => true,
  purge_services   => true,
  purge_ports      => true,
  icmp_blocks      => 'router-advertisement'
}
```

#### Properties

The following properties are available in the `firewalld_zone` type.

##### `ensure`

Valid values: present, absent

The basic property that the resource should be in.

Default value: present

##### `target`

Specify the target for the zone

##### `interfaces`

Specify the interfaces for the zone

##### `masquerade`

Valid values: `true`, `false`

Can be set to true or false, specifies whether to add or remove masquerading from the zone

##### `sources`

Specify the sources for the zone

##### `icmp_blocks`

Specify the icmp-blocks for the zone. Can be a single string specifying one icmp type,
or an array of strings specifying multiple icmp types. Any blocks not specified here will be removed

##### `purge_rich_rules`

Valid values: `false`, `true`

When set to true any rich_rules associated with this zone
that are not managed by Puppet will be removed.

##### `purge_services`

Valid values: `false`, `true`

When set to true any services associated with this zone
that are not managed by Puppet will be removed.

##### `purge_ports`

Valid values: `false`, `true`

When set to true any ports associated with this zone
that are not managed by Puppet will be removed.

#### Parameters

The following parameters are available in the `firewalld_zone` type.

##### `name`

namevar

Name of the rule resource in Puppet

##### `zone`

Name of the zone

##### `description`

Description of the zone to add

##### `short`

Short description of the zone to add

