# Heimy HashLips Doge Edition My Tweaks To Hashlips For The Doge Blockchain 🔥

## 🚀 Getting Started

### **1️⃣ Download & Install**
1. Clone the repository or download the folder.
2. Ensure **Node.js** is installed.
3. Open the folder in **VS Code** or **Terminal**.
4. Run:
   ```sh
   npm install
   ```

### **2️⃣ Prepare Your Layers**
- Place all layer images in the `layers/` directory.
- Name the folders according to their layer type, e.g., `Background`, `Skin`, `Head`.
- Ensure each layer has a **rarity** out of 100:
  ```sh
  blue#20.png  # Blue background used in 20% of the collection.
  ```
- Each folder's layers **must total 100%** to distribute traits correctly.

### **3️⃣ Configure Your Collection**

#### **🔹 Set Collection Name**
```js
const namePrefix = "Your name here";
```
Open `config.js` and edit:

#### **🔹 Define Layer Order & Collection Size**
```js
const layerConfigurations = [
  {
    growEditionSizeTo: 50,  // Set collection size
    layersOrder: [
      { name: "Background" },
      { name: "Body" },
      { name: "Skin" },
      { name: "Head" }
    ]
  }
];
```

#### **🔹 Set Image Dimensions**
```js
const format = {
  width: 400,  // Match layer resolution
  height: 400,
  smoothing: false,
};
```

#### **🔹 Standard Generation Settings**
```js
const convertFilenames = false;
const recursion = false;
```

### **4️⃣ Generate the Collection**
Run the command:
```sh
npm run build
```
Your **generated collection** will be in the `build/` folder:
- **Images** → `/build/images`
- **Metadata** → `/build/json` (for marketplaces: Doggy Market & Ordinals Wallet)

### **5️⃣ Inscribing Your Collection**
Once images are generated, **inscribe them** on-chain.
📩 **DM me on X: [@heimdall_bull](https://twitter.com/heimdall_bull)** for inscription services.
After inscribing, update the metadata with **inscription IDs** before listing.

---

## 🌀 Creating a Recursive Collection

### **1️⃣ Inscribe Your Layers**
- **Each layer must be inscribed individually**.
- They will be named numerically (`00001.png`, `00002.png`, etc.).
- Add all numbered assets to respective layer folders.

### **2️⃣ Create `layerconfig.json`**
This file **maps filenames to trait names and inscription IDs**:
```json
[
  { "filename": "00001", "layername": "Blue", "inscriptionId": "INSCRIPTION_ID" },
  { "filename": "00002", "layername": "Green", "inscriptionId": "INSCRIPTION_ID" },
  { "filename": "00003", "layername": "Yellow", "inscriptionId": "INSCRIPTION_ID" }
]
```
**Ensure:**
- All assets are correctly mapped.
- No **conflicts or overlapping traits**.

### **3️⃣ Enable Recursive Mode**
Update `config.js`:
```js
const convertFilenames = true;
const recursion = true;
```
Save the file.

### **4️⃣ Generate the Recursive Collection**
Run:
```sh
npm run build
```
This time, your build will contain:
- **Images** → `/build/images` (for marketing & previewing).
- **HTML Files** → `/build/html` (ready for inscription).
- **Metadata** → `/build/json/`
  - `DM.json` → For **Doggy Market**.
  - `OW.json` → For **Ordinals Wallet**.

### **5️⃣ Final Step: Inscribe & Submit Metadata**
1. **Inscribe all generated HTML files**.
2. **Update `DM.json` & `OW.json`** with the **inscription IDs**.
3. **Submit the metadata to the relevant marketplaces**.

📩 **For inscription assistance, contact me on X: [@heimdall_bull](https://twitter.com/heimdall_bull)**.

🎉 **You're now ready to launch your recursive NFT collection!** 🚀


---
---

full hashlips instructions below for all features


Create generative art by using the canvas api and node js. Before you use the generation engine, make sure you have node.js(v10.18.0) installed.

## Installation 🛠️

Download this Github - open it in vs code or in the command line 

Go to the root of your folder and run this command if you have yarn installed.

```sh
yarn install
```

Alternatively you can run this command if you have node installed.

```sh
npm install
```

## Usage ℹ️

Create your different layers as folders in the 'layers' directory, and add all the layer assets in these directories. 
You can name the assets anything as long as it has a rarity weight attached in the file name like so: `example element#70.png`. 
You can optionally change the delimiter `#` to anything you would like to use in the variable `rarityDelimiter` in the `src/config.js` file.

Once you have all your layers, 

go into `src/config.js` and update the `layerConfigurations` objects `layersOrder` array to be your layer folders name in order of the back layer to the front layer.

_Example:_ If you were creating a portrait design, you might have a background, then a head, a mouth, eyes, eyewear, and then headwear, so your `layersOrder` would look something like this:

```js
const layerConfigurations = [
  {
    growEditionSizeTo: 100,
    layersOrder: [
      { name: "Background" },
      { name: "Head" },
      { name: "Mouth" },
      { name: "Eyes" },
      { name: "Eyeswear" },
      { name: "Headwear" },
    ],
  },
];
```

The `name` of each layer object represents the name of the folder (in `/layers/`) that the images reside in.

Optionally you can now add multiple different `layerConfigurations` to your collection. Each configuration can be unique and have different layer orders, use the same layers or introduce new ones. This gives the artist flexibility when it comes to fine tuning their collections to their needs.

_Example:_ If you were creating a portrait design, you might have a background, then a head, a mouth, eyes, eyewear, and then headwear and you want to create a new race or just simple re-order the layers or even introduce new layers, then you're `layerConfigurations` and `layersOrder` would look something like this:

```js
const layerConfigurations = [
  {
    // Creates up to 50 artworks
    growEditionSizeTo: 50,
    layersOrder: [
      { name: "Background" },
      { name: "Head" },
      { name: "Mouth" },
      { name: "Eyes" },
      { name: "Eyeswear" },
      { name: "Headwear" },
    ],
  },
  {
    // Creates an additional 100 artworks
    growEditionSizeTo: 150,
    layersOrder: [
      { name: "Background" },
      { name: "Head" },
      { name: "Eyes" },
      { name: "Mouth" },
      { name: "Eyeswear" },
      { name: "Headwear" },
      { name: "AlienHeadwear" },
    ],
  },
];
```

Update your `format` size, ie the outputted image size, and the `growEditionSizeTo` on each `layerConfigurations` object, which is the amount of variation outputted.

You can mix up the `layerConfigurations` order on how the images are saved by setting the variable `shuffleLayerConfigurations` in the `config.js` file to true. It is false by default and will save all images in numerical order.

If you want to have logs to debug and see what is happening when you generate images you can set the variable `debugLogs` in the `config.js` file to true. It is false by default, so you will only see general logs.

If you want to play around with different blending modes, you can add a `blend: MODE.colorBurn` field to the layersOrder `options` object.

If you need a layers to have a different opacity then you can add the `opacity: 0.7` field to the layersOrder `options` object as well.

If you want to have a layer _ignored_ in the DNA uniqueness check, you can set `bypassDNA: true` in the `options` object. This has the effect of making sure the rest of the traits are unique while not considering the `Background` Layers as traits, for example. The layers _are_ included in the final image.

To use a different metadata attribute name you can add the `displayName: "Awesome Eye Color"` to the `options` object. All options are optional and can be addes on the same layer if you want to.

Here is an example on how you can play around with both filter fields:

```js
const layerConfigurations = [
  {
    growEditionSizeTo: 5,
    layersOrder: [
      { name: "Background" , {
        options: {
          bypassDNA: false;
        }
      }},
      { name: "Eyeball" },
      {
        name: "Eye color",
        options: {
          blend: MODE.destinationIn,
          opacity: 0.2,
          displayName: "Awesome Eye Color",
        },
      },
      { name: "Iris" },
      { name: "Shine" },
      { name: "Bottom lid", options: { blend: MODE.overlay, opacity: 0.7 } },
      { name: "Top lid" },
    ],
  },
];
```

Here is a list of the different blending modes that you can optionally use.

```js
const MODE = {
  sourceOver: "source-over",
  sourceIn: "source-in",
  sourceOut: "source-out",
  sourceAtop: "source-out",
  destinationOver: "destination-over",
  destinationIn: "destination-in",
  destinationOut: "destination-out",
  destinationAtop: "destination-atop",
  lighter: "lighter",
  copy: "copy",
  xor: "xor",
  multiply: "multiply",
  screen: "screen",
  overlay: "overlay",
  darken: "darken",
  lighten: "lighten",
  colorDodge: "color-dodge",
  colorBurn: "color-burn",
  hardLight: "hard-light",
  softLight: "soft-light",
  difference: "difference",
  exclusion: "exclusion",
  hue: "hue",
  saturation: "saturation",
  color: "color",
  luminosity: "luminosity",
};
```

When you are ready, run the following command and your outputted art will be in the `build/images` directory and the json in the `build/json` directory:

```sh
npm run build
```

or

```sh
node index.js
```

The program will output all the images in the `build/images` directory along with the metadata files in the `build/json` directory. Each collection will have a `_metadata.json` file that consists of all the metadata in the collection inside the `build/json` directory. The `build/json` folder also will contain all the single json files that represent each image file. The single json file of a image will look something like this:

```json
{
  "dna": "d956cdf4e460508b5ff90c21974124f68d6edc34",
  "name": "#1",
  "description": "This is the description of your NFT project",
  "image": "https://hashlips/nft/1.png",
  "edition": 1,
  "date": 1731990799975,
  "attributes": [
    { "trait_type": "Background", "value": "Black" },
    { "trait_type": "Eyeball", "value": "Red" },
    { "trait_type": "Eye color", "value": "Yellow" },
    { "trait_type": "Iris", "value": "Small" },
    { "trait_type": "Shine", "value": "Shapes" },
    { "trait_type": "Bottom lid", "value": "Low" },
    { "trait_type": "Top lid", "value": "Middle" }
  ],
  "compiler": "HashLips Art Engine"
}
```

You can also add extra metadata to each metadata file by adding your extra items, (key: value) pairs to the `extraMetadata` object variable in the `config.js` file.

```js
const extraMetadata = {
  creator: "Daniel Eugene Botha",
};
```

If you don't need extra metadata, simply leave the object empty. It is empty by default.

```js
const extraMetadata = {};
```

That's it, you're done.


### Generate a preview image

Create a preview image collage of your collection, run:

```sh
npm run preview
```

### Generate pixelated images from collection

In order to convert images into pixelated images you would need a list of images that you want to convert. So run the generator first.

Then simply run this command:

```sh
npm run pixelate
```

All your images will be outputted in the `/build/pixel_images` directory.
If you want to change the ratio of the pixelation then you can update the ratio property on the `pixelFormat` object in the `src/config.js` file. The lower the number on the left, the more pixelated the image will be.

```js
const pixelFormat = {
  ratio: 5 / 128,
};
```

### Generate GIF images from collection

In order to export gifs based on the layers created, you just need to set the export on the `gif` object in the `src/config.js` file to `true`. You can also play around with the `repeat`, `quality` and the `delay` of the exported gif.

Setting the `repeat: -1` will produce a one time render and `repeat: 0` will loop forever.

```js
const gif = {
  export: true,
  repeat: 0,
  quality: 100,
  delay: 500,
};
```

### Printing rarity data (Experimental feature)

To see the percentages of each attribute across your collection, run:

```sh
npm run rarity
```

The output will look something like this:

```sh
Trait type: Top lid
{
  trait: 'High',
  chance: '30',
  occurrence: '3 in 20 editions (15.00 %)'
}
{
  trait: 'Low',
  chance: '20',
  occurrence: '3 in 20 editions (15.00 %)'
}
{
  trait: 'Middle',
  chance: '50',
  occurrence: '14 in 20 editions (70.00 %)'
}
```

Hope you create some awesome artworks with this code 👄
