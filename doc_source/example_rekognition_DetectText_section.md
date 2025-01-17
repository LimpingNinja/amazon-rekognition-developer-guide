# Detect text in an image with Amazon Rekognition using an AWS SDK<a name="example_rekognition_DetectText_section"></a>

The following code examples show how to detect text in an image with Amazon Rekognition\.

For more information, see [Detecting text in an image](https://docs.aws.amazon.com/rekognition/latest/dg/text-detecting-text-procedure.html)\.

------
#### [ \.NET ]

**AWS SDK for \.NET**  
  

```
        public static async Task Main()
        {
            string photo = "Dad_photographer.jpg"; // "input.jpg";
            string bucket = "igsmiths3photos"; // "bucket";

            var rekognitionClient = new AmazonRekognitionClient();

            var detectTextRequest = new DetectTextRequest()
            {
                Image = new Image()
                {
                    S3Object = new S3Object()
                    {
                        Name = photo,
                        Bucket = bucket,
                    },
                },
            };

            try
            {
                DetectTextResponse detectTextResponse = await rekognitionClient.DetectTextAsync(detectTextRequest);
                Console.WriteLine($"Detected lines and words for {photo}");
                detectTextResponse.TextDetections.ForEach(text =>
                {
                    Console.WriteLine($"Detected: {text.DetectedText}");
                    Console.WriteLine($"Confidence: {text.Confidence}");
                    Console.WriteLine($"Id : {text.Id}");
                    Console.WriteLine($"Parent Id: {text.ParentId}");
                    Console.WriteLine($"Type: {text.Type}");
                });
            }
            catch (Exception e)
            {
                Console.WriteLine(e.Message);
            }
        }
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/dotnetv3/Rekognition/#code-examples)\. 
+  For API details, see [DetectText](https://docs.aws.amazon.com/goto/DotNetSDKV3/rekognition-2016-06-27/DetectText) in *AWS SDK for \.NET API Reference*\. 

------
#### [ Java ]

**SDK for Java 2\.x**  
  

```
    public static void detectTextLabels(RekognitionClient rekClient, String sourceImage) {

        try {

            InputStream sourceStream = new FileInputStream(sourceImage);
            SdkBytes sourceBytes = SdkBytes.fromInputStream(sourceStream);

            // Create an Image object for the source image
            Image souImage = Image.builder()
                    .bytes(sourceBytes)
                    .build();

            DetectTextRequest textRequest = DetectTextRequest.builder()
                    .image(souImage)
                   .build();

            DetectTextResponse textResponse = rekClient.detectText(textRequest);
            List<TextDetection> textCollection = textResponse.textDetections();

            System.out.println("Detected lines and words");
            for (TextDetection text: textCollection) {
                System.out.println("Detected: " + text.detectedText());
                System.out.println("Confidence: " + text.confidence().toString());
                System.out.println("Id : " + text.id());
                System.out.println("Parent Id: " + text.parentId());
                System.out.println("Type: " + text.type());
                System.out.println();
            }

           } catch (RekognitionException | FileNotFoundException e) {
            System.out.println(e.getMessage());
            System.exit(1);
        }
    }
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/javav2/example_code/rekognition/#readme)\. 
+  For API details, see [DetectText](https://docs.aws.amazon.com/goto/SdkForJavaV2/rekognition-2016-06-27/DetectText) in *AWS SDK for Java 2\.x API Reference*\. 

------
#### [ Kotlin ]

**SDK for Kotlin**  
This is prerelease documentation for a feature in preview release\. It is subject to change\.
  

```
suspend fun detectTextLabels(sourceImage: String?) {

        val souImage = Image {
            bytes = (File(sourceImage).readBytes())
        }

        val request = DetectTextRequest {
            image = souImage
        }

        RekognitionClient { region = "us-east-1" }.use { rekClient ->
          val response = rekClient.detectText(request)
          response.textDetections?.forEach { text ->
                 println("Detected: ${text.detectedText}")
                println("Confidence: ${text.confidence}")
                println("Id: ${text.id}")
                println("Parent Id:  ${text.parentId}")
                println("Type: ${text.type}")
          }
        }
}
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/kotlin/services/rekognition#code-examples)\. 
+  For API details, see [DetectText](https://github.com/awslabs/aws-sdk-kotlin#generating-api-documentation) in *AWS SDK for Kotlin API reference*\. 

------
#### [ Python ]

**SDK for Python \(Boto3\)**  
  

```
class RekognitionImage:
    """
    Encapsulates an Amazon Rekognition image. This class is a thin wrapper
    around parts of the Boto3 Amazon Rekognition API.
    """
    def __init__(self, image, image_name, rekognition_client):
        """
        Initializes the image object.

        :param image: Data that defines the image, either the image bytes or
                      an Amazon S3 bucket and object key.
        :param image_name: The name of the image.
        :param rekognition_client: A Boto3 Rekognition client.
        """
        self.image = image
        self.image_name = image_name
        self.rekognition_client = rekognition_client

    def detect_text(self):
        """
        Detects text in the image.

        :return The list of text elements found in the image.
        """
        try:
            response = self.rekognition_client.detect_text(Image=self.image)
            texts = [RekognitionText(text) for text in response['TextDetections']]
            logger.info("Found %s texts in %s.", len(texts), self.image_name)
        except ClientError:
            logger.exception("Couldn't detect text in %s.", self.image_name)
            raise
        else:
            return texts
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/python/example_code/rekognition#code-examples)\. 
+  For API details, see [DetectText](https://docs.aws.amazon.com/goto/boto3/rekognition-2016-06-27/DetectText) in *AWS SDK for Python \(Boto3\) API Reference*\. 

------

For a complete list of AWS SDK developer guides and code examples, including help getting started and information about previous versions, see [Using Rekognition with an AWS SDK](sdk-general-information-section.md)\.