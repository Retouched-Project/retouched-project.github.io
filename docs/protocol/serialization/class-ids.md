# Class ID Registry

Every `Externalizable` class in BM has a fixed **class ID** (i16). The class ID appears in the [object envelope](object-encoding.md) and tells the deserializer which class to instantiate.

## How It Works

Both the sender and receiver maintain an identical registry that maps class IDs to class implementations. This registry is populated at startup and must be consistent across all SDK implementations for communication to succeed.

When deserializing, the process is:

1. Read the class ID from the object envelope.
2. Look up the class ID in the registry.
3. Create a new instance of that class.
4. Call `readExternal()` on the instance to read its fields.

If a class ID is not found in the registry, deserialization fails.

## Class ID Table

See the [Class ID Reference Table](../../reference/class-ids.md) for the complete mapping of class IDs to object types.

## Notes

- Class ID **0** is used by `BMPacket`. ID **256** is registered as an alias for `BMPacket` in the Android SDK.
- Class IDs are protocol-defined constants. They are not negotiated or exchanged dynamically.
- Device subclasses (e.g. `AndroidDevice`, `FlashDevice`) have their own class IDs (10, 18, etc.) distinct from the base `Device` class.