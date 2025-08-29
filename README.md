# change-string-case-action-min-dependencies
Github Action: Make a string lowercase, uppercase, or capitalized

this runs in pure python without any additional packages or dependencies!

# Change String Case GitHub Action

This action accepts any string, and outputs three different versions of that string:

- lowercase (`XyZzY` -> `xyzzy`)
- uppercase (`XyZzY` -> `XYZZY`)
- capitalized (`Xyzzy` -> `Xyzzy`)
- dashnormalized (`Xy.ZzY` -> `xy-zzy`)

You can access the outputted strings through the job outputs context. See docs [here](https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions#jobsjobs_idoutputs), or the Example Usage section below.

## Inputs

### `string`

**Required** The string you want manipulated

## Outputs

### `lowercase`

```python
lowercase="${{ inputs.string }}".lower()
```

Example: `XyZzY` -> `xyzzy`

### `uppercase`

```python
uppercase="${{ inputs.string }}".upper()
```

Example: `XyZzY` -> `XYZZY`

### `capitalized`

```python
lowercase="${{ inputs.string }}".lower()
uppercase="${{ inputs.string }}".upper()
capitalized=f'{uppercase[:1]}{lowercase[1:]}'
```

Example: `XyZzY` -> `Xyzzy`

### `dashnormalized`

```python
lowercase="${{ inputs.string }}".lower()
dashnormalized=''.join(x if x.isalnum() else '-' for x in lowercase)
```

Example: `Xy.ZzY` -> `xy-zzy`

### `afterlastdash`

```python
afterlastdash="${{ inputs.string }}".split("/")[-1]
```

### `lowerlastdash`

```python
lowerlastdash="${{ inputs.string }}".split("/")[-1].lower()
```


## Example Usage

```yaml
name: SomeWorkflow
jobs:
  build:
    name: Build
    runs-on: ubuntu-latest
    steps:
      - id: string
        uses: Entepotenz/change-string-case-action-min-dependencies@v1
        with:
          string: XyZzY
      - id: step2
        run: echo ${{ steps.string.outputs.lowercase }}
      - id: step3
        run: echo ${{ steps.string.outputs.uppercase }}
      - id: step4
        run: echo ${{ steps.string.outputs.capitalized }}
      - id: step5
        run: echo ${{ steps.string.outputs.dashnormalized }}
      - id: step6
        run: echo ${{ steps.string.outputs.afterlastdash }}
      - id: step7
        run: echo ${{ steps.string.outputs.lowerlastdash }}
```
