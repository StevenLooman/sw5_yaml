# SW5 YAML encoder/decoder

YAML encoder/decoder for Smallworld 5/Magik.

## Introduction

Smallworld Magik encoder/decoer for YAML. This product currently supports *parts* of the [YAML 1.2.2 specification](https://yaml.org/spec/1.2.2/), not the complete specification. This product will most likely parse invalid YAML documents without any warning, or not parse valid YAML documents when it contains certain YAML features. Your milage may vary.

## Usage

The YAML encoder/decoder is built after the Smallworld 5 `sw:json_encoder`/`sw:json_decoder`. The same API applies for the `myaml:yaml_encoder`/`myaml:yaml_decoder`. Example usage of the `myaml:yaml_encoder`:

```magik
Magik> enc << myaml:yaml_encoder.new()
a myaml:yaml_encoder
Magik> data << equality_property_list.new_with("key1", "value1", "key2", rope.new_with("a", "b"))
equality_property_list(2)
Magik> str << enc.generate_string(data)
"key1: value1<newline>key2:<newline>  - a<newline>  - b"
Magik> write(str)
key1: value1
key2:
  - a
  - b
Magik>
```

Example usage of the `myaml:yaml_decoder`:

```magik
Magik> dec << myaml:yaml_decoder.new()
a myaml:yaml_encoder
Magik> str << write_string(
  "key1: value1", character.newline,
  "key2:", character.newline,
  "  - a", character.newline,
  "  - b")
"key1: value1<newline>key2:<newline>  - a<newline>  - b"
magik> dec.parse_string(str)
concurrent_hash_map(2)
Magik> print(!)
concurrent_hash_map:
:key2   sw:rope:[1-2]
:key1   "value1"
```

## Testing

MUnit is used for tests.

## Contributing

Currently no contributions are accepted in the form of Pull Requests. Bug reports are welcome, but there is no guarantee these will be picked up.

## License

This product is licensed under GPLv3. If you need a custom license, please contact me.
