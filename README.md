PAGE.Image adds image functionality to the global PAGE object. Currently it only handles SVG's, but this will be expanded. PAGE.Image takes advantage of the extend functionality of the PAGE object to add methods to it. It depends upon PAGE.Dispatcher, which handles async calls to load files.

Simple example
```JavaScript

		PAGE.add("Modules.Demo", (function() {
			var dog = {
				$images : $("#images")
				, all : {}
			}

			PAGE.wait("Image", function(Image) {

				dog.Image = Image
				dog.Images = PAGE.Images

				for(var y = 1; y < 78; y++) {
					var $image = dog.all["SVG/image_" + y + ".svg"] = $("<span class='wrap'>")
					dog.$images.append($image)
				}

				Image.addWaitSVGBatch(dog.all, function($item, index, src) {
					dog.all[src].append($item.clone())
				}, function(newBatch) {
					console.info("finished loading")
					alert("finished loading")
				})

			})

			return dog
		}()))

```

Run the demo in a browser. Type PAGE.Modules.Demo into the javascript console.
