# Detect moderation labels in an image with Amazon Rekognition using an AWS SDK<a name="example_rekognition_DetectModerationLabels_section"></a>

The following code examples show how to detect moderation labels in an image with Amazon Rekognition\. Moderation labels identify content that may be inappropriate for some audiences\.

For more information, see [Detecting inappropriate images](https://docs.aws.amazon.com/rekognition/latest/dg/procedure-moderate-images.html)\.

------
#### [ \.NET ]

**AWS SDK for \.NET**  
  

```
        public static async Task Main(string[] args)
        {
            string photo = "input.jpg";
            string bucket = "bucket";

            var rekognitionClient = new AmazonRekognitionClient();

            var detectModerationLabelsRequest = new DetectModerationLabelsRequest()
            {
                Image = new Image()
                {
                    S3Object = new S3Object()
                    {
                        Name = photo,
                        Bucket = bucket,
                    },
                },
                MinConfidence = 60F,
            };

            try
            {
                var detectModerationLabelsResponse = await rekognitionClient.DetectModerationLabelsAsync(detectModerationLabelsRequest);
                Console.WriteLine("Detected labels for " + photo);
                foreach (ModerationLabel label in detectModerationLabelsResponse.ModerationLabels)
                {
                    Console.WriteLine($"Label: {label.Name}");
                    Console.WriteLine($"Confidence: {label.Confidence}");
                    Console.WriteLine($"Parent: {label.ParentName}");
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.Message);
            }
        }
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/dotnetv3/Rekognition/#code-examples)\. 
+  For API details, see [DetectModerationLabels](https://docs.aws.amazon.com/goto/DotNetSDKV3/rekognition-2016-06-27/DetectModerationLabels) in *AWS SDK for \.NET API Reference*\. 

------
#### [ Java ]

**SDK for Java 2\.x**  
  

```
    public static void detectModLabels(RekognitionClient rekClient, String sourceImage) {

    try {
        InputStream sourceStream = new FileInputStream(sourceImage);
        SdkBytes sourceBytes = SdkBytes.fromInputStream(sourceStream);

        Image souImage = Image.builder()
                .bytes(sourceBytes)
                .build();

        DetectModerationLabelsRequest moderationLabelsRequest = DetectModerationLabelsRequest.builder()
                .image(souImage)
                .minConfidence(60F)
                .build();

        DetectModerationLabelsResponse moderationLabelsResponse = rekClient.detectModerationLabels(moderationLabelsRequest);

        // Display the results
        List<ModerationLabel> labels = moderationLabelsResponse.moderationLabels();
        System.out.println("Detected labels for image");

        for (ModerationLabel label : labels) {
            System.out.println("Label: " + label.name()
                    + "\n Confidence: " + label.confidence().toString() + "%"
                    + "\n Parent:" + label.parentName());
        }

    } catch (RekognitionException | FileNotFoundException e) {
        e.printStackTrace();
        System.exit(1);
    }
  }
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/javav2/example_code/rekognition/#readme)\. 
+  For API details, see [DetectModerationLabels](https://docs.aws.amazon.com/goto/SdkForJavaV2/rekognition-2016-06-27/DetectModerationLabels) in *AWS SDK for Java 2\.x API Reference*\. 

------
#### [ Kotlin ]

**SDK for Kotlin**  
This is prerelease documentation for a feature in preview release\. It is subject to change\.
  

```
suspend fun detectModLabels(sourceImage: String) {

        val myImage = Image {
            this.bytes = (File(sourceImage).readBytes())
        }

        val request = DetectModerationLabelsRequest {
            image = myImage
            minConfidence = 60f
        }

        RekognitionClient { region = "us-east-1" }.use { rekClient ->
          val response = rekClient.detectModerationLabels(request)
          response.moderationLabels?.forEach { label ->
              println("Label: ${label.name} - Confidence: ${label.confidence} % Parent: ${label.parentName}")
           }
       }
}
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/kotlin/services/rekognition#code-examples)\. 
+  For API details, see [DetectModerationLabels](https://github.com/awslabs/aws-sdk-kotlin#generating-api-documentation) in *AWS SDK for Kotlin API reference*\. 

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

    def detect_moderation_labels(self):
        """
        Detects moderation labels in the image. Moderation labels identify content
        that may be inappropriate for some audiences.

        :return: The list of moderation labels found in the image.
        """
        try:
            response = self.rekognition_client.detect_moderation_labels(
                Image=self.image)
            labels = [RekognitionModerationLabel(label)
                      for label in response['ModerationLabels']]
            logger.info(
                "Found %s moderation labels in %s.", len(labels), self.image_name)
        except ClientError:
            logger.exception(
                "Couldn't detect moderation labels in %s.", self.image_name)
            raise
        else:
            return labels
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/python/example_code/rekognition#code-examples)\. 
+  For API details, see [DetectModerationLabels](https://docs.aws.amazon.com/goto/boto3/rekognition-2016-06-27/DetectModerationLabels) in *AWS SDK for Python \(Boto3\) API Reference*\. 

------

For a complete list of AWS SDK developer guides and code examples, including help getting started and information about previous versions, see [Using Rekognition with an AWS SDK](sdk-general-information-section.md)\.