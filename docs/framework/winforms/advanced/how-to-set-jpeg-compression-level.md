---
title: 如何：設定 JPEG 壓縮層級
description: 瞭解如何藉由修改 Windows Forms 上的壓縮層級，來調整 JPEG 影像的品質。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- images [Windows Forms], changing encoder parameters
- JPEG images [Windows Forms], setting quality level
ms.assetid: 4b9a74e3-9504-43c1-9f28-ace651d0772e
ms.openlocfilehash: 1f6a96e8a05fff40eb08da0ce318faa86a06cc3a
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85618710"
---
# <a name="how-to-set-jpeg-compression-level"></a><span data-ttu-id="e3a2d-103">如何：設定 JPEG 壓縮層級</span><span class="sxs-lookup"><span data-stu-id="e3a2d-103">How to: Set JPEG Compression Level</span></span>
<span data-ttu-id="e3a2d-104">當您將影像儲存至磁碟以減少檔案大小或改善其品質時，可能會想要修改影像的參數。</span><span class="sxs-lookup"><span data-stu-id="e3a2d-104">You may want to modify the parameters of an image when you save the image to disk to minimize the file size or improve its quality.</span></span> <span data-ttu-id="e3a2d-105">您可以修改其壓縮層級來調整 JPEG 影像的品質。</span><span class="sxs-lookup"><span data-stu-id="e3a2d-105">You can adjust the quality of a JPEG image by modifying its compression level.</span></span> <span data-ttu-id="e3a2d-106">若要在儲存 JPEG 影像時指定壓縮等級，您必須建立 <xref:System.Drawing.Imaging.EncoderParameters> 物件，並將它傳遞給 <xref:System.Drawing.Image.Save%2A> 類別的方法 <xref:System.Drawing.Image> 。</span><span class="sxs-lookup"><span data-stu-id="e3a2d-106">To specify the compression level when you save a JPEG image, you must create an <xref:System.Drawing.Imaging.EncoderParameters> object and pass it to the <xref:System.Drawing.Image.Save%2A> method of the <xref:System.Drawing.Image> class.</span></span> <span data-ttu-id="e3a2d-107">初始化 <xref:System.Drawing.Imaging.EncoderParameters> 物件，使其具有由一個組成的陣列 <xref:System.Drawing.Imaging.EncoderParameter> 。</span><span class="sxs-lookup"><span data-stu-id="e3a2d-107">Initialize the <xref:System.Drawing.Imaging.EncoderParameters> object so that it has an array that consists of one <xref:System.Drawing.Imaging.EncoderParameter>.</span></span> <span data-ttu-id="e3a2d-108">當您建立時 <xref:System.Drawing.Imaging.EncoderParameter> ，請指定 <xref:System.Drawing.Imaging.Encoder.Quality> 編碼器和所需的壓縮等級。</span><span class="sxs-lookup"><span data-stu-id="e3a2d-108">When you create the <xref:System.Drawing.Imaging.EncoderParameter>, specify the <xref:System.Drawing.Imaging.Encoder.Quality> encoder, and the desired compression level.</span></span>  
  
## <a name="example"></a><span data-ttu-id="e3a2d-109">範例</span><span class="sxs-lookup"><span data-stu-id="e3a2d-109">Example</span></span>  
 <span data-ttu-id="e3a2d-110">下列範例程式碼會建立 <xref:System.Drawing.Imaging.EncoderParameter> 物件，並儲存三個 JPEG 影像。</span><span class="sxs-lookup"><span data-stu-id="e3a2d-110">The following example code creates an <xref:System.Drawing.Imaging.EncoderParameter> object and saves three JPEG images.</span></span> <span data-ttu-id="e3a2d-111">每個 JPEG 影像都會以不同的品質層級儲存，方法是修改 `long` 傳遞給此函式的值 <xref:System.Drawing.Imaging.EncoderParameter> 。</span><span class="sxs-lookup"><span data-stu-id="e3a2d-111">Each JPEG image is saved with a different quality level, by modifying the `long` value passed to the <xref:System.Drawing.Imaging.EncoderParameter> constructor.</span></span> <span data-ttu-id="e3a2d-112">品質層級 0 對應到最大壓縮，而品質層級 100 對應到最小壓縮。</span><span class="sxs-lookup"><span data-stu-id="e3a2d-112">A quality level of 0 corresponds to the greatest compression, and a quality level of 100 corresponds to the least compression.</span></span>  
  
```csharp  
private void VaryQualityLevel()  
    {  
        // Get a bitmap. The using statement ensures objects  
        // are automatically disposed from memory after use.  
        using (Bitmap bmp1 = new Bitmap(@"C:\TestPhoto.jpg"))  
        {  
            ImageCodecInfo jpgEncoder = GetEncoder(ImageFormat.Jpeg);  
  
            // Create an Encoder object based on the GUID  
            // for the Quality parameter category.  
            System.Drawing.Imaging.Encoder myEncoder =  
                System.Drawing.Imaging.Encoder.Quality;  
  
            // Create an EncoderParameters object.  
            // An EncoderParameters object has an array of EncoderParameter  
            // objects. In this case, there is only one  
            // EncoderParameter object in the array.  
            EncoderParameters myEncoderParameters = new EncoderParameters(1);  
  
            EncoderParameter myEncoderParameter = new EncoderParameter(myEncoder, 50L);  
            myEncoderParameters.Param[0] = myEncoderParameter;  
            bmp1.Save(@"c:\TestPhotoQualityFifty.jpg", jpgEncoder, myEncoderParameters);  
  
            myEncoderParameter = new EncoderParameter(myEncoder, 100L);  
            myEncoderParameters.Param[0] = myEncoderParameter;  
            bmp1.Save(@"C:\TestPhotoQualityHundred.jpg", jpgEncoder, myEncoderParameters);  
  
            // Save the bitmap as a JPG file with zero quality level compression.  
            myEncoderParameter = new EncoderParameter(myEncoder, 0L);  
            myEncoderParameters.Param[0] = myEncoderParameter;  
            bmp1.Save(@"C:\TestPhotoQualityZero.jpg", jpgEncoder, myEncoderParameters);  
        }  
    }  
```  
  
```vb  
Private Sub VaryQualityLevel()  
    ' Get a bitmap. The Using statement ensures objects  
    ' are automatically disposed from memory after use.  
    Using bmp1 As New Bitmap("C:\test\TestPhoto.jpg")  
        Dim jpgEncoder As ImageCodecInfo = GetEncoder(ImageFormat.Jpeg)  
  
        ' Create an Encoder object based on the GUID  
        ' for the Quality parameter category.  
        Dim myEncoder As System.Drawing.Imaging.Encoder = System.Drawing.Imaging.Encoder.Quality  
  
        ' Create an EncoderParameters object.  
        ' An EncoderParameters object has an array of EncoderParameter  
        ' objects. In this case, there is only one  
        ' EncoderParameter object in the array.  
        Dim myEncoderParameters As New EncoderParameters(1)  
  
        Dim myEncoderParameter As New EncoderParameter(myEncoder, 50L)  
        myEncoderParameters.Param(0) = myEncoderParameter  
        bmp1.Save("c:\test\TestPhotoQualityFifty.jpg", jpgEncoder, myEncoderParameters)  
  
        myEncoderParameter = New EncoderParameter(myEncoder, 100L)  
        myEncoderParameters.Param(0) = myEncoderParameter  
        bmp1.Save("C:\test\TestPhotoQualityHundred.jpg", jpgEncoder, myEncoderParameters)  
  
        ' Save the bitmap as a JPG file with zero quality level compression.  
        myEncoderParameter = New EncoderParameter(myEncoder, 0L)  
        myEncoderParameters.Param(0) = myEncoderParameter  
        bmp1.Save("C:\test\TestPhotoQualityZero.jpg", jpgEncoder, myEncoderParameters)  
    End Using  
End Sub  
```  
  
```csharp  
private ImageCodecInfo GetEncoder(ImageFormat format)  
{  
    ImageCodecInfo[] codecs = ImageCodecInfo.GetImageDecoders();  
    foreach (ImageCodecInfo codec in codecs)  
    {  
        if (codec.FormatID == format.Guid)  
        {  
            return codec;  
        }  
    }  
    return null;  
}  
```  
  
```vb  
Private Function GetEncoder(ByVal format As ImageFormat) As ImageCodecInfo  
  
    Dim codecs As ImageCodecInfo() = ImageCodecInfo.GetImageDecoders()  
    Dim codec As ImageCodecInfo  
    For Each codec In codecs  
        If codec.FormatID = format.Guid Then  
            Return codec  
        End If  
    Next codec  
    Return Nothing  
  
End Function  
```  
  
## <a name="compiling-the-code"></a><span data-ttu-id="e3a2d-113">編譯程式碼</span><span class="sxs-lookup"><span data-stu-id="e3a2d-113">Compiling the Code</span></span>  
 <span data-ttu-id="e3a2d-114">這個範例需要：</span><span class="sxs-lookup"><span data-stu-id="e3a2d-114">This example requires:</span></span>  
  
- <span data-ttu-id="e3a2d-115">Windows Forms 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e3a2d-115">A Windows Forms application.</span></span>  
  
- <span data-ttu-id="e3a2d-116"><xref:System.Windows.Forms.PaintEventArgs>，它是的參數 <xref:System.Windows.Forms.PaintEventHandler> 。</span><span class="sxs-lookup"><span data-stu-id="e3a2d-116">A <xref:System.Windows.Forms.PaintEventArgs>, which is a parameter of <xref:System.Windows.Forms.PaintEventHandler>.</span></span>  
  
- <span data-ttu-id="e3a2d-117">名為 `TestPhoto.jpg` 且位在 **c:\\** 的影像檔。</span><span class="sxs-lookup"><span data-stu-id="e3a2d-117">An image file that is named `TestPhoto.jpg` and located at **c:\\**.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e3a2d-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e3a2d-118">See also</span></span>

- [<span data-ttu-id="e3a2d-119">如何：判斷編碼器所支援的參數</span><span class="sxs-lookup"><span data-stu-id="e3a2d-119">How to: Determine the Parameters Supported by an Encoder</span></span>](how-to-determine-the-parameters-supported-by-an-encoder.md)
- [<span data-ttu-id="e3a2d-120">點陣圖類型</span><span class="sxs-lookup"><span data-stu-id="e3a2d-120">Types of Bitmaps</span></span>](types-of-bitmaps.md)
- [<span data-ttu-id="e3a2d-121">使用 Managed GDI+ 中的影像編碼器和解碼器</span><span class="sxs-lookup"><span data-stu-id="e3a2d-121">Using Image Encoders and Decoders in Managed GDI+</span></span>](using-image-encoders-and-decoders-in-managed-gdi.md)
