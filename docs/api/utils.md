# utils

## `validateAddress`

### Function Signature
```typescript
function validateAddress(address: string | null | undefined, allowZeroAddress: boolean = false): boolean
```

### Description
The `validateAddress` function checks if a given Ethereum address is valid. It ensures the address is a properly formatted hex string and optionally checks if the zero address is allowed.

### Parameters
- `address`: The Ethereum address to validate. It can be a string, null, or undefined.
- `allowZeroAddress`: A boolean indicating whether the zero address (`0x0000000000000000000000000000000000000000`) is allowed. Defaults to `false`.

### Returns
- Returns `true` if the address is valid.

### Throws
- Throws an `Error` if:
  - The `address` is `null` or `undefined`.
    - Example: `Error: Address cannot be null or undefined`
  - The `address` does not start with `0x` or is not 42 characters long.
    - Example: `Error: Invalid address format. Must be a hex string starting with 0x`
  - The `address` contains invalid characters (not 0-9, a-f, A-F).
    - Example: `Error: Invalid address characters`
  - The `address` is the zero address and `allowZeroAddress` is `false`.
    - Example: `Error: Zero address not allowed`

### Example Usage
```typescript
try {
  const isValid = validateAddress('0x1234567890abcdef1234567890abcdef12345678');
  console.log('Address is valid:', isValid);
} catch (error) {
  console.error('Validation error:', error.message);
}

try {
  const isValid = validateAddress('0x0000000000000000000000000000000000000000', true);
  console.log('Zero address is valid:', isValid);
} catch (error) {
  console.error('Validation error:', error.message);
}
```

## `isAGWAccount`

### Function Signature
```typescript
async function isAGWAccount<Transport, chain>(
  publicClient: PublicClient<Transport, chain>,
  address: Address,
  timeoutMs: number = 5000
): Promise<boolean>
```

### Description
The `isAGWAccount` function checks if a given address is an Abstract Global Wallet (AGW) account. It includes a timeout feature to prevent long waits for a response.

### Parameters
- `publicClient`: The client used to interact with the blockchain.
- `address`: The address to check.
- `timeoutMs`: The maximum time in milliseconds to wait for a response. Defaults to 5000ms.

### Returns
- Returns `true` if the address is an AGW account.

### Throws
- Throws an `Error` if the operation times out.
  - Example: `Error: isAGWAccount check timed out`

### Example Usage
```typescript
try {
  const isAgw = await isAGWAccount(publicClient, '0x1234567890abcdef1234567890abcdef12345678');
  console.log('Is AGW account:', isAgw);
} catch (error) {
  console.error('Error checking AGW account:', error.message);
}
```

## `getAgwTypedSignature`

### Function Signature
```typescript
async function getAgwTypedSignature(
  args: GetAgwTypedSignatureParams
): Promise<Hex>
```

### Description
The `getAgwTypedSignature` function generates a typed signature for a given message hash, with support for custom domain versions.

### Parameters
- `args`: An object containing:
  - `client`: The client used to interact with the blockchain.
  - `signer`: The wallet client used to sign the message.
  - `messageHash`: The hash of the message to sign. Must be a 32-byte hex string.
  - `domainVersion`: Optional. The version of the domain. Defaults to "2.0.0".

### Returns
- Returns a `Hex` string representing the signature.

### Throws
- Throws an `Error` if the `messageHash` format is invalid.
  - Example: `Error: Invalid messageHash format. Must be a 32-byte hex string starting with 0x`

### Example Usage
```typescript
try {
  const signature = await getAgwTypedSignature({
    client,
    signer,
    messageHash: '0xabcdefabcdefabcdefabcdefabcdefabcdefabcdefabcdefabcdefabcdefabcdef',
    domainVersion: '1.0.0'
  });
  console.log('Signature:', signature);
} catch (error) {
  console.error('Error generating signature:', error.message);
}
```

These updates reflect the recent changes in the SDK, providing users with enhanced validation and timeout handling features.