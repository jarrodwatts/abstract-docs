# CHANGELOG

## Version 1.4.5 - 2023-10-15

### New Features

#### `validateAddress` Function Update
- **Null/Undefined Handling**: The `validateAddress` function now accepts `null` or `undefined` as input for the `address` parameter and throws an error if these values are provided.
- **Hex Validation**: Added a check to ensure the address contains only valid hex characters (0-9, a-f, A-F).

**Function Signature:**
```typescript
export function validateAddress(address: string | null | undefined, allowZeroAddress: boolean = false): boolean
```

**Usage Example:**
```typescript
try {
  validateAddress('0x1234567890abcdef1234567890abcdef12345678');
} catch (error) {
  console.error(error.message);
}
```

**Error Conditions:**
- If `address` is `null` or `undefined`: 
  - Error: `'Address cannot be null or undefined'`
- If `address` does not start with '0x' or is not 42 characters long:
  - Error: `'Invalid address format. Must be a hex string starting with 0x'`
- If `address` contains invalid characters:
  - Error: `'Invalid address characters'`
- If `allowZeroAddress` is `false` and `address` is the zero address:
  - Error: `'Zero address not allowed'`

### Enhancements

#### `isAGWAccount` Function Update
- **Timeout Parameter**: Added a `timeoutMs` parameter to the `isAGWAccount` function to specify a timeout for the contract read operation.

**Function Signature:**
```typescript
export async function isAGWAccount<Transport, chain>(
  publicClient: PublicClient<Transport, chain>,
  address: Address,
  timeoutMs: number = 5000
): Promise<boolean>
```

**Usage Example:**
```typescript
try {
  const isAccount = await isAGWAccount(client, '0x1234567890abcdef1234567890abcdef12345678', 3000);
} catch (error) {
  console.error(error.message); // 'isAGWAccount check timed out'
}
```

**Error Conditions:**
- If the operation times out:
  - Error: `'isAGWAccount check timed out'`

### Bug Fixes

#### `getAgwTypedSignature` Function Update
- **Message Hash Validation**: Added validation for the `messageHash` parameter to ensure it is a 32-byte hex string.

**Function Signature:**
```typescript
export async function getAgwTypedSignature(
  args: GetAgwTypedSignatureParams
): Promise<Hex>
```

**Usage Example:**
```typescript
try {
  const signature = await getAgwTypedSignature({
    client,
    signer,
    messageHash: '0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef'
  });
} catch (error) {
  console.error(error.message); // 'Invalid messageHash format. Must be a 32-byte hex string starting with 0x'
}
```

**Error Conditions:**
- If `messageHash` is not a valid 32-byte hex string:
  - Error: `'Invalid messageHash format. Must be a 32-byte hex string starting with 0x'`

For more details, refer to the [API documentation](https://docs.abs.xyz/api).