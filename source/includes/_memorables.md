# Memorables

## What is a `memorable`?
A memorable is an abstract model that represents content within Everalbum. It is the base class which is inherited by the three concrete models explained below.

### `Item`
(Should just be called a "photo")

### `Flipbook`
A collection of photos (items). These are displayed as an animation, similar to an Animated GIF (pronounced 'JIF'))

A Flipbook contains images (minimum of three) that were taken within a few moments of each other in the same aspect ratio

### `Video`
Just a video :)


## Memorable Creation Request

`POST http://API_URL/memorables.json`

<br />

`memorables` are created on the server before the image or video itself is uploaded for a couple reasons:<br />
<ul>
  <li>We can cluster photos on the user's behalf before the content is uploaded and create albums for them based on metadata</li>
  <li>We can help the client determine the best order in which the photos should be eventually uploaded for a better experience</li>
</ul>

<br />

The `memorable` creation process and payload can differ slightly per client:<br />
<ul>
  <li>Some clients will detect and create their own flipbooks (iOS for instance)</li>
  <li>The source field is different based on the client that creates the memorables</li>
</ul>

### Base Request Parameters

```json
{
   "create_flipbooks":false,
   "timezone":"-08:00",
   "memorables":[
     memorable_payloads
   ]
}
```

The basic structure of this request looks like this:

Parameter | Required? | Default | Description
--------- | --------- | ------- | -----------
create_flipbooks | NO | true | If set to false, the client is responsible for sending flipbook payloads to /memorables.json endpoint
timezone | NO | "-08:00" | If not net, the server will use PST
memorables | YES | NULL | An array of memorable payloads as detailed below

### Memorable Creation Payloads

Each type of memorable, `item`, `flipbook`, `video` has a specific payload which defines how it will be created.

### Item Payload

```json
{
   "aspect_ratio":"1.505618",
   "captured_at":"2011-03-12 16:17:25",
   "latitude":"38.03745",
   "longitude":"-122.8032",
   "original_asset_quickhash":"ddaa2610cbd4f2591af15dbbb9850a61",
   "source":"mobile",
   "type":"Item"
}
```
Each `Item` payload should consist of the following:

Parameter | Required? | Default | Description
--------- | --------- | ------- | -----------
aspect_ratio | YES | NULL | The aspect ratio of the image (width / height)
captured_at | YES | NULL | The image's EXIF date (when the image was taken)
latitude | NO | NULL | The latitude of where the image was taken
longitude | NO | NULL | The longitude of where the image was taken
source | YES | NULL | Options are currently [ desktop / mobile ]
type | YES | NULL | Should be set to "Item" when creating photo memorables
original_asset_quickhash | NO | NULL | A hash of a collection of metadata to uniquely identify an image
original_asset_md5 | NO | NULL | The MD5 hash of the image this memorable represents

You're only required to provide `original_asset_quickhash` OR `original_asset_md5` when creating Items. You may provide both if you choose.

### Flipbook Payload

```json
{
   "source":"mobile",
   "type":"Flipbook",
   "flipbook_memorables_ordered_quickhashes":[
      "a98dcdcd597e7f15b9d0056da1a2b964",
      "b37a6e7035eaa96f670dbdd70754ed6b",
      "12235f1573c63dac436cb8738e2deb42",
      "80c52c14df5fc97da0c38f403d33b461"
   ]
}
```

Each `Flipbook` payload should consist of the following:

Parameter | Required? | Default | Description
--------- | --------- | ------- | -----------
source | YES | NULL | Options are currently [ desktop / mobile ]
type | YES | NULL | Should be set to "Item" when creating photo memorables
flipbook_memorables_ordered_quickhashes | YES | NULL | A list of the quickhashes for items that belong in this flipbook (ordered by captured_at)

Each `item` represented within `flipbook_memorables_ordered_quickhashes` should be listed before the `flipbook` that contains them in the payload of the `POST` to `/memorables.json`

### Video Payload

```json
{
   "aspect_ratio":"1.699",
   "captured_at":"2012-08-08 11:52:11",
   "latitude":"65.68289",
   "longitude":"-17.54893",
   "original_asset_quickhash":"abc123abc73b83d542c17deb71774920",
   "source":"mobile",
   "type":"Video"
}
```

Each `Video` payload should consist of the following:

Parameter | Required? | Default | Description
--------- | --------- | ------- | -----------
aspect_ratio | YES | NULL | The aspect ratio of the video (width / height)
captured_at | YES | NULL | The video's date (when the video was taken)
latitude | NO | NULL | The latitude of where the video was taken
longitude | NO | NULL | The longitude of where the video was taken
original_asset_quickhash | NO | NULL | A hash of a collection of metadata to uniquely identify an video
original_asset_md5 | NO | NULL | The MD5 hash of the video this memorable represents
source | YES | NULL | Options are currently [ desktop / mobile ]
type | YES | NULL | Should be set to "Video" when creating video memorables

You're only required to provide `original_asset_quickhash` OR `original_asset_md5` when creating Videos. You may provide both if you choose.

### Complete Request

```json
{
   "create_flipbooks":false,
   "memorables":[
      {
         "aspect_ratio":"1.333333",
         "captured_at":"2015-09-26 17:31:49",
         "latitude":"20.92027",
         "longitude":"-156.6951",
         "original_asset_quickhash":"a98dcdcd597e7f15b9d0056da1a2b964",
         "source":"mobile",
         "type":"Item"
      },
      {
         "aspect_ratio":"1.333333",
         "captured_at":"2015-09-26 17:31:49",
         "latitude":"20.92027",
         "longitude":"-156.6951",
         "original_asset_quickhash":"b37a6e7035eaa96f670dbdd70754ed6b",
         "source":"mobile",
         "type":"Item"
      },
      {
         "aspect_ratio":"1.333333",
         "captured_at":"2015-09-26 17:31:49",
         "latitude":"20.92027",
         "longitude":"-156.6951",
         "original_asset_quickhash":"12235f1573c63dac436cb8738e2deb42",
         "source":"mobile",
         "type":"Item"
      },
      {
         "aspect_ratio":"1.333333",
         "captured_at":"2015-09-26 17:31:49",
         "latitude":"20.92027",
         "longitude":"-156.6951",
         "original_asset_quickhash":"80c52c14df5fc97da0c38f403d33b461",
         "source":"mobile",
         "type":"Item"
      },
      {
         "aspect_ratio":"1.505618",
         "captured_at":"2011-03-12 16:17:25",
         "latitude":"38.03745",
         "longitude":"-122.8032",
         "original_asset_quickhash":"ddaa2610cbd4f2591af15dbbb9850a61",
         "source":"mobile",
         "type":"Item"
      },
      {
         "aspect_ratio":"1.699",
         "captured_at":"2012-08-08 11:52:11",
         "latitude":"65.68289",
         "longitude":"-17.54893",
         "original_asset_quickhash":"abc123abc73b83d542c17deb71774920",
         "source":"mobile",
         "type":"Video"
      },
      {
         "flipbook_memorables_ordered_quickhashes":[
            "a98dcdcd597e7f15b9d0056da1a2b964",
            "b37a6e7035eaa96f670dbdd70754ed6b",
            "12235f1573c63dac436cb8738e2deb42",
            "80c52c14df5fc97da0c38f403d33b461"
         ],
         "source":"mobile",
         "type":"Flipbook"
      }
   ],
   "timezone":"-08:00"
}
```

This is an example of a complete request to create `memorables`.

The request consists of:<br />
<ul>
  <li>5 Images</li>
  <li>1 Video</li>
  <li>1 Flipbook (containing 4 of the 5 images)</li>
</ul>

<br />

Notice the order in which the `memorables` are listed to be created:<br />
<ol>
  <li>Items</li>
  <li>Videos</li>
  <li>Flipbooks</li>
</ol>

## Memorable Creation Response

```json
[
   {
      "aspect_ratio":"1.33",
      "captured_at":"2015-09-26 17:31:49",
      "has_active_asset":false,
      "has_original_asset":false,
      "id":202907,
      "original_asset_md5":null,
      "original_asset_quickhash":"12235f1573c63dac436cb8738e2deb42",
      "type":"Item"
   },
   {
      "aspect_ratio":"1.33",
      "captured_at":"2015-09-26 17:31:49",
      "has_active_asset":false,
      "has_original_asset":false,
      "id":202899,
      "original_asset_md5":null,
      "original_asset_quickhash":"80c52c14df5fc97da0c38f403d33b461",
      "type":"Item"
   },
   {
      "aspect_ratio":"1.33",
      "captured_at":"2015-09-26 17:31:49",
      "has_active_asset":false,
      "has_original_asset":false,
      "id":202900,
      "original_asset_md5":null,
      "original_asset_quickhash":"a98dcdcd597e7f15b9d0056da1a2b964",
      "type":"Item"
   },
   {
      "aspect_ratio":"1.33",
      "captured_at":"2015-09-26 17:31:49",
      "has_active_asset":false,
      "has_original_asset":false,
      "id":202903,
      "original_asset_md5":null,
      "original_asset_quickhash":"b37a6e7035eaa96f670dbdd70754ed6b",
      "type":"Item"
   },
   {
      "aspect_ratio":"1.51",
      "captured_at":"2011-03-12 16:17:25",
      "has_active_asset":false,
      "has_original_asset":false,
      "id":202901,
      "original_asset_md5":null,
      "original_asset_quickhash":"ddaa2610cbd4f2591af15dbbb9850a61",
      "type":"Item"
   },
   {
      "aspect_ratio":"1.699",
      "captured_at":"2012-08-08 11:52:11",
      "has_active_asset":false,
      "has_original_asset":false,
      "id":202902,
      "original_asset_md5":null,
      "original_asset_quickhash":"abc123abc73b83d542c17deb71774920",
      "type":"Video"
   },
   {
      "aspect_ratio":"1.33",
      "captured_at":"2015-09-26 17:31:49",
      "flipbook_memorables":[
         {
            "id":33340,
            "memorable_id":202903
         },
         {
            "id":33339,
            "memorable_id":202900
         },
         {
            "id":33338,
            "memorable_id":202899
         },
         {
            "id":33337,
            "memorable_id":202907
         }
      ],
      "id":202908,
      "type":"Flipbook"
   }
]
```

The response contains a variety of parameters about a `memorable`. The most important one that clients will be interested in is the `id` parameter. This is the new remote identifier that the backend will identify the `memorable` by
