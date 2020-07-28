# About

Ansible role `ansible-swap`
Install, setup and run zSwap and zRAM as systemd service for VM and BareMetal servers.

## Requirements

- systemd

## Role variables

### Defaults

```yaml
---
# defaults file for ansible-swap
dpkg_force_overwrite_configs: false

# swapfile
swap_file_enabled: false
# Use any of the following suffixes
# c=1
# w=2
# b=512
# kB=1000
# K=1024
# MB=1000*1000
# M=1024*1024
# xM=M
# GB=1000*1000*1000
# G=1024*1024*1024
swap_file_path: '/swapfile'
swap_file_size: '2G'


# systemd-swap
swap_systemd_enabled: true
swap_systemd_package:
  name: 'systemd-swap'
  version: '4.0.2'
  deb: 'systemd-swap_4.0.2_all.deb'

# zSwap
swap_systemd_zswap_enabled: false
swap_systemd_zswap_max_pool_percent: 20

# zRam
swap_systemd_zram_enabled: false
# swap_systemd_zram_size: "{{ (( ansible_memtotal_mb * 1024 * 1024 | filesizeformat | human_to_bytes ) / 2 ) | int | abs }}" # in bytes
# swap_systemd_zram_count: "{{ ( ansible_processor_vcpus / 2 ) | int | abs }}"
# swap_systemd_zram_streams: "{{ ansible_processor_vcpus }}"
swap_systemd_zram_size: '$(( ${RAM_SIZE} / 2 ))'
swap_systemd_zram_count: '${NCPU}'
swap_systemd_zram_streams: '${NCPU}'

# Swap File Chunks
swap_systemd_swapfc_enabled: false
swap_systemd_swapfc_force_use_loop: true
swap_systemd_swapfc_chunk_size: '512M'
swap_systemd_swapfc_max_count: 8 # 1..32
swap_systemd_swapfc_free_swap_perc: 15

# Swap Device
swap_systemd_swapd_auto_swapon: true
```

## Dependencies

-

## Example playbook

```yaml
- hosts: servers
  roles:
    - role: ansible-swap
```

## License

MIT
