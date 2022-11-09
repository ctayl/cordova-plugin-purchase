# Class: Store

[CdvPurchase](../modules/CdvPurchase.md).Store

Entry class of the plugin.

## Table of contents

### Constructors

- [constructor](CdvPurchase.Store.md#constructor)

### Properties

- [applicationUsername](CdvPurchase.Store.md#applicationusername)
- [log](CdvPurchase.Store.md#log)
- [validator](CdvPurchase.Store.md#validator)
- [validator\_privacy\_policy](CdvPurchase.Store.md#validator_privacy_policy)
- [verbosity](CdvPurchase.Store.md#verbosity)
- [version](CdvPurchase.Store.md#version)

### Accessors

- [localReceipts](CdvPurchase.Store.md#localreceipts)
- [localTransactions](CdvPurchase.Store.md#localtransactions)
- [products](CdvPurchase.Store.md#products)
- [verifiedPurchases](CdvPurchase.Store.md#verifiedpurchases)
- [verifiedReceipts](CdvPurchase.Store.md#verifiedreceipts)

### Methods

- [error](CdvPurchase.Store.md#error)
- [findInLocalReceipts](CdvPurchase.Store.md#findinlocalreceipts)
- [findInVerifiedReceipts](CdvPurchase.Store.md#findinverifiedreceipts)
- [finish](CdvPurchase.Store.md#finish)
- [get](CdvPurchase.Store.md#get)
- [getAdapter](CdvPurchase.Store.md#getadapter)
- [getApplicationUsername](CdvPurchase.Store.md#getapplicationusername)
- [initialize](CdvPurchase.Store.md#initialize)
- [manageSubscriptions](CdvPurchase.Store.md#managesubscriptions)
- [order](CdvPurchase.Store.md#order)
- [owned](CdvPurchase.Store.md#owned)
- [ready](CdvPurchase.Store.md#ready)
- [refresh](CdvPurchase.Store.md#refresh)
- [register](CdvPurchase.Store.md#register)
- [requestPayment](CdvPurchase.Store.md#requestpayment)
- [restorePurchases](CdvPurchase.Store.md#restorepurchases)
- [update](CdvPurchase.Store.md#update)
- [when](CdvPurchase.Store.md#when)
- [defaultPlatform](CdvPurchase.Store.md#defaultplatform)

## Constructors

### constructor

• **new Store**()

## Properties

### applicationUsername

• `Optional` **applicationUsername**: `string` \| () => `string`

Return the identifier of the user for your application

___

### log

• **log**: [`Logger`](CdvPurchase.Logger.md)

Logger

___

### validator

• **validator**: `undefined` \| `string` \| [`Function`](../interfaces/CdvPurchase.Validator.Function.md) \| [`Target`](../interfaces/CdvPurchase.Validator.Target.md)

URL or implementation of the receipt validation service

**`Example`**

Define the validator as a string
```ts
CdvPurchase.store.validator = "https://validator.iaptic.com/v1/validate?appName=test"
```

**`Example`**

Define the validator as a function
```ts
CdvPurchase.store.validator = (receipt, callback) => {
  callback({
    ok: true,
    data: {
      // see CdvPurchase.Validator.Response.Payload for details
    }
  })
}
```

**`See`**

[Payload](../modules/CdvPurchase.Validator.Response.md#payload)

___

### validator\_privacy\_policy

• **validator\_privacy\_policy**: `undefined` \| [`PrivacyPolicyItem`](../modules/CdvPurchase.md#privacypolicyitem) \| [`PrivacyPolicyItem`](../modules/CdvPurchase.md#privacypolicyitem)[]

When adding information to receipt validation requests, those can serve different functions:

 - handling support requests
 - fraud detection
 - analytics
 - tracking

Make sure the value your select is in line with your application's privacy policy and your users' tracking preference.

**`Example`**

```ts
CdvPurchase.store.validator_privacy_policy = [
  'fraud', 'support', 'analytics', 'tracking'
]
```

___

### verbosity

• **verbosity**: [`LogLevel`](../enums/CdvPurchase.LogLevel.md) = `LogLevel.ERROR`

Verbosity level used by the plugin logger

Set to:

 - LogLevel.QUIET or 0 to disable all logging (default)
 - LogLevel.ERROR or 1 to show only error messages
 - LogLevel.WARNING or 2 to show warnings and errors
 - LogLevel.INFO or 3 to also show information messages
 - LogLevel.DEBUG or 4 to enable internal debugging messages.

**`See`**

[LogLevel](../enums/CdvPurchase.LogLevel.md)

___

### version

• **version**: `string` = `PLUGIN_VERSION`

## Accessors

### localReceipts

• `get` **localReceipts**(): [`Receipt`](CdvPurchase.Receipt.md)[]

List of all receipts as present on the device.

#### Returns

[`Receipt`](CdvPurchase.Receipt.md)[]

___

### localTransactions

• `get` **localTransactions**(): [`Transaction`](CdvPurchase.Transaction.md)[]

List of all transaction from the local receipts.

#### Returns

[`Transaction`](CdvPurchase.Transaction.md)[]

___

### products

• `get` **products**(): [`Product`](CdvPurchase.Product.md)[]

List of all active products

#### Returns

[`Product`](CdvPurchase.Product.md)[]

___

### verifiedPurchases

• `get` **verifiedPurchases**(): [`VerifiedPurchase`](../interfaces/CdvPurchase.VerifiedPurchase.md)[]

List of all purchases from the verified receipts.

#### Returns

[`VerifiedPurchase`](../interfaces/CdvPurchase.VerifiedPurchase.md)[]

___

### verifiedReceipts

• `get` **verifiedReceipts**(): [`VerifiedReceipt`](CdvPurchase.VerifiedReceipt.md)[]

List of receipts verified with the receipt validation service.

Those receipt contains more information and are generally more up-to-date than the local ones.

#### Returns

[`VerifiedReceipt`](CdvPurchase.VerifiedReceipt.md)[]

## Methods

### error

▸ **error**(`error`): `void`

#### Parameters

| Name | Type |
| :------ | :------ |
| `error` | [`IError`](../interfaces/CdvPurchase.IError.md) \| [`Callback`](../modules/CdvPurchase.md#callback)<[`IError`](../interfaces/CdvPurchase.IError.md)\> |

#### Returns

`void`

___

### findInLocalReceipts

▸ **findInLocalReceipts**(`product`): `undefined` \| [`Transaction`](CdvPurchase.Transaction.md)

Find the latest transaction for a given product, from those reported by the device.

#### Parameters

| Name | Type |
| :------ | :------ |
| `product` | [`Product`](CdvPurchase.Product.md) |

#### Returns

`undefined` \| [`Transaction`](CdvPurchase.Transaction.md)

___

### findInVerifiedReceipts

▸ **findInVerifiedReceipts**(`product`): `undefined` \| [`VerifiedPurchase`](../interfaces/CdvPurchase.VerifiedPurchase.md)

Find the last verified purchase for a given product, from those verified by the receipt validator.

#### Parameters

| Name | Type |
| :------ | :------ |
| `product` | [`Product`](CdvPurchase.Product.md) |

#### Returns

`undefined` \| [`VerifiedPurchase`](../interfaces/CdvPurchase.VerifiedPurchase.md)

___

### finish

▸ **finish**(`receipt`): `Promise`<`void`\>

Finalize a transaction

#### Parameters

| Name | Type |
| :------ | :------ |
| `receipt` | [`Receipt`](CdvPurchase.Receipt.md) \| [`Transaction`](CdvPurchase.Transaction.md) \| [`VerifiedReceipt`](CdvPurchase.VerifiedReceipt.md) |

#### Returns

`Promise`<`void`\>

___

### get

▸ **get**(`productId`, `platform?`): `undefined` \| [`Product`](CdvPurchase.Product.md)

Find a product from its id and platform

#### Parameters

| Name | Type |
| :------ | :------ |
| `productId` | `string` |
| `platform` | [`Platform`](../enums/CdvPurchase.Platform.md) |

#### Returns

`undefined` \| [`Product`](CdvPurchase.Product.md)

___

### getAdapter

▸ **getAdapter**(`platform`): `undefined` \| [`Adapter`](../interfaces/CdvPurchase.Adapter.md)

Retrieve a platform adapter.

The platform adapter has to have been initialized before.

**`See`**

[initialize](CdvPurchase.Store.md#initialize)

#### Parameters

| Name | Type |
| :------ | :------ |
| `platform` | [`Platform`](../enums/CdvPurchase.Platform.md) |

#### Returns

`undefined` \| [`Adapter`](../interfaces/CdvPurchase.Adapter.md)

___

### getApplicationUsername

▸ **getApplicationUsername**(): `undefined` \| `string`

Get the application username as a string by either calling or returning [applicationUsername](CdvPurchase.Store.md#applicationusername)

#### Returns

`undefined` \| `string`

___

### initialize

▸ **initialize**(`platforms?`): `Promise`<[`IError`](../interfaces/CdvPurchase.IError.md)[]\>

Call to initialize the in-app purchase plugin.

#### Parameters

| Name | Type | Description |
| :------ | :------ | :------ |
| `platforms` | ([`Platform`](../enums/CdvPurchase.Platform.md) \| [`PlatformWithOptions`](../modules/CdvPurchase.md#platformwithoptions))[] | List of payment platforms to initialize, default to Store.defaultPlatform(). |

#### Returns

`Promise`<[`IError`](../interfaces/CdvPurchase.IError.md)[]\>

___

### manageSubscriptions

▸ **manageSubscriptions**(`platform?`): `Promise`<`undefined` \| [`IError`](../interfaces/CdvPurchase.IError.md)\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `platform?` | [`Platform`](../enums/CdvPurchase.Platform.md) |

#### Returns

`Promise`<`undefined` \| [`IError`](../interfaces/CdvPurchase.IError.md)\>

___

### order

▸ **order**(`offer`, `additionalData?`): `Promise`<`undefined` \| [`IError`](../interfaces/CdvPurchase.IError.md)\>

Place an order for a given offer

#### Parameters

| Name | Type |
| :------ | :------ |
| `offer` | [`Offer`](CdvPurchase.Offer.md) |
| `additionalData?` | [`AdditionalData`](../interfaces/CdvPurchase.AdditionalData.md) |

#### Returns

`Promise`<`undefined` \| [`IError`](../interfaces/CdvPurchase.IError.md)\>

___

### owned

▸ **owned**(`product`): `boolean`

Return true if a product is owned

#### Parameters

| Name | Type | Description |
| :------ | :------ | :------ |
| `product` | `string` \| { `id`: `string` ; `platform?`: [`Platform`](../enums/CdvPurchase.Platform.md)  } | The product object or identifier of the product. |

#### Returns

`boolean`

___

### ready

▸ **ready**(`cb`): `void`

Register a callback to be called when the plugin is ready.

#### Parameters

| Name | Type |
| :------ | :------ |
| `cb` | [`Callback`](../modules/CdvPurchase.md#callback)<`void`\> |

#### Returns

`void`

___

### refresh

▸ **refresh**(): `void`

**`Deprecated`**

- use store.initialize(), store.update() or store.restorePurchases()

#### Returns

`void`

___

### register

▸ **register**(`product`): `void`

Register a product.

**`Example`**

```ts
store.register([{
      id: 'subscription1',
      type: ProductType.PAID_SUBSCRIPTION,
      platform: Platform.APPLE_APPSTORE,
  }, {
      id: 'subscription1',
      type: ProductType.PAID_SUBSCRIPTION,
      platform: Platform.GOOGLE_PLAY,
  }, {
      id: 'consumable1',
      type: ProductType.CONSUMABLE,
      platform: Platform.BRAINTREE,
  }]);
```

#### Parameters

| Name | Type |
| :------ | :------ |
| `product` | [`IRegisterProduct`](../interfaces/CdvPurchase.IRegisterProduct.md) \| [`IRegisterProduct`](../interfaces/CdvPurchase.IRegisterProduct.md)[] |

#### Returns

`void`

___

### requestPayment

▸ **requestPayment**(`paymentRequest`, `additionalData?`): `Promise`<`undefined` \| [`IError`](../interfaces/CdvPurchase.IError.md)\>

Request a payment

#### Parameters

| Name | Type |
| :------ | :------ |
| `paymentRequest` | [`PaymentRequest`](../interfaces/CdvPurchase.PaymentRequest.md) |
| `additionalData?` | [`AdditionalData`](../interfaces/CdvPurchase.AdditionalData.md) |

#### Returns

`Promise`<`undefined` \| [`IError`](../interfaces/CdvPurchase.IError.md)\>

___

### restorePurchases

▸ **restorePurchases**(): `Promise`<`void`\>

#### Returns

`Promise`<`void`\>

___

### update

▸ **update**(): `Promise`<`void`\>

Call to refresh the price of products and status of purchases.

#### Returns

`Promise`<`void`\>

___

### when

▸ **when**(): [`When`](../interfaces/CdvPurchase.When.md)

Setup events listener.

**`Example`**

```ts
store.when()
     .productUpdated(product => updateUI(product))
     .approved(transaction => store.finish(transaction));
```

#### Returns

[`When`](../interfaces/CdvPurchase.When.md)

___

### defaultPlatform

▸ `Static` **defaultPlatform**(): [`Platform`](../enums/CdvPurchase.Platform.md)

The default payment platform to use depending on the OS.

- on iOS: `APPLE_APPSTORE`
- on Android: `GOOGLE_PLAY`

#### Returns

[`Platform`](../enums/CdvPurchase.Platform.md)