# zerotier-hosts action

This action allows you retrive all hosts(members) in a specific zerotier network.

## Inputs

## `network-id`

**Required** The network ID. You network ID can be found in [ZeroTier Networks](https://my.zerotier.com/network)

## `api-access-token`

**Required** The API Access token for zerotier API. You can generate it from [ZeroTier Account](https://my.zerotier.com/account)

## `format`

**Required** The hosts info output format. Can be `plain` or `json`. Default it is `plain`.

For example if your network has two members:

|Node ID|Name|IP|
|---|---|---|
|xxxxabc|laptop|192.168.1.111|
|xxxxdef|camera|192.168.1.112|


- If the `format` is set to `plain`, the output of `hosts` is a plain text string contains like bellow.

    ```plain
    xxxxabc 192.168.1.111
    laptop 192.168.1.111
    xxxxdef 192.168.1.112
    camera 192.168.1.112
    ```

- If the `format` is set to `json`, the output of `hosts` is a json string like bellow.

    ```json
    [
        {"host":"xxxxabc", "address": "192.168.1.111"},
        {"host":"laptop", "address": "192.168.1.111"},
        {"host":"xxxxdef", "address": "192.168.1.112"},
        {"host":"camera", "address": "192.168.1.112"}
    ]
    ```

## Outputs

## `hosts`

The hosts info of zerotier network.

## Example Usage

```yaml
  - name: zerotier-hosts action step
    uses: ian4hu/zerotier-hosts@v1.0.0
    id: plain
    with:
        network-id: ${{ secrets.NETWORK_ID }}
        api-access-token: ${{ secrets.API_ACCESS_TOKEN }}
        format: 'plain'
  - name: Get the output hosts
    run: echo "The hosts was ${{ steps.plain.outputs.hosts }}"
  - name: zerotier-hosts action step
    uses: ian4hu/zerotier-hosts@v1.0.0
    id: json
    with:
        network-id: ${{ secrets.NETWORK_ID }}
        api-access-token: ${{ secrets.API_ACCESS_TOKEN }}
        format: 'json'
  - name: Get the output hosts
    run: echo "The hosts was ${{ steps.json.outputs.hosts }}"
```