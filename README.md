- 👋 Hi, I’m @komal787
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
komal787/komal787 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import org.opencv.core.Core;
import org.opencv.core.Mat;
import org.opencv.core.MatOfRect;
import org.opencv.core.Point;
import org.opencv.core.Scalar;
import org.opencv.core.Size;
import org.opencv.imgcodecs.Imgcodecs;
import org.opencv.imgproc.Imgproc;
import org.opencv.objdetect.CascadeClassifier;

public class FaceRecognitionApp {
    public static void main(String[] args) {
        System.loadLibrary(Core.NATIVE_LIBRARY_NAME);

        // Load the face detection XML file (you can replace this with your own trained model)
        CascadeClassifier faceCascade = new CascadeClassifier("haarcascade_frontalface_default.xml");

        // Load the image
        Mat image = Imgcodecs.imread("path_to_your_image.jpg");

        // Convert the image to grayscale (required for face detection)
        Mat grayImage = new Mat();
        Imgproc.cvtColor(image, grayImage, Imgproc.COLOR_BGR2GRAY);

        // Detect faces in the image
        MatOfRect faceDetections = new MatOfRect();
        faceCascade.detectMultiScale(grayImage, faceDetections);

        System.out.println("Number of faces detected: " + faceDetections.toArray().length);

        // Draw rectangles around detected faces
        for (org.opencv.core.Rect rect : faceDetections.toArray()) {
            Imgproc.rectangle(image, new Point(rect.x, rect.y), new Point(rect.x + rect.width, rect.y + rect.height),
                    new Scalar(0, 255, 0), 3);
        }

        // Save the output image
        Imgcodecs.imwrite("output_image.jpg", image);
    }
}
