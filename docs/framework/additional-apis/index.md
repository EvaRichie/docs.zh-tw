---
title: 其他類別庫和 API
description: 探索 .NET 中的其他類別庫和 Api，包括頻外（OOB）專案、平臺特定程式庫和私用 Api。
ms.date: 06/12/2020
helpviewer_keywords:
- Additional class libraries
- Additional managed libraries
- .NET Framework out-of-band releases
- out-of-band releases
ms.assetid: cf2d9006-b631-4e5d-81cd-20aab78c60f1
ms.topic: conceptual
ms.openlocfilehash: 0b888d2f0e80685ba993682b2f3067cf8aee15bc
ms.sourcegitcommit: 45c8eed045779b70a47b23169897459d0323dc89
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "84989740"
---
# <a name="additional-class-libraries-and-apis"></a><span data-ttu-id="13572-103">其他類別庫和 API</span><span class="sxs-lookup"><span data-stu-id="13572-103">Additional class libraries and APIs</span></span>

<span data-ttu-id="13572-104">這篇文章列出已發行頻外、以特定平臺為目標，或為私用或內部類型的 .NET Framework Api。</span><span class="sxs-lookup"><span data-stu-id="13572-104">This article lists .NET Framework APIs that either were released out of band, target a specific platform, or are private or internal types.</span></span>

## <a name="oob-projects"></a><span data-ttu-id="13572-105">OOB 專案</span><span class="sxs-lookup"><span data-stu-id="13572-105">OOB projects</span></span>

<span data-ttu-id="13572-106">為了改善跨平臺開發並及早引進新功能，有些 .NET Framework 功能已發行頻外（OOB）。</span><span class="sxs-lookup"><span data-stu-id="13572-106">To improve cross-platform development and introduce new functionality early, some .NET Framework features were released out of band (OOB).</span></span>

| <span data-ttu-id="13572-107">Project</span><span class="sxs-lookup"><span data-stu-id="13572-107">Project</span></span> | <span data-ttu-id="13572-108">描述</span><span class="sxs-lookup"><span data-stu-id="13572-108">Description</span></span> |  
| ------- | ----------- |  
| <xref:System.Collections.Immutable> | <span data-ttu-id="13572-109">提供具備執行緒安全且保證不會再變更其內容的集合。</span><span class="sxs-lookup"><span data-stu-id="13572-109">Provides collections that are thread safe and guaranteed to never change their contents.</span></span> |
| <xref:System.Net.Http.WinHttpHandler> | <span data-ttu-id="13572-110">提供以 Windows 的 WinHTTP 介面為基礎之 <xref:System.Net.Http.HttpClient> 的訊息處理常式。</span><span class="sxs-lookup"><span data-stu-id="13572-110">Provides a message handler for <xref:System.Net.Http.HttpClient> based on the WinHTTP interface of Windows.</span></span> |
| <xref:System.Numerics> | <span data-ttu-id="13572-111">提供可利用 SIMD 硬體加速的向量類型程式庫。</span><span class="sxs-lookup"><span data-stu-id="13572-111">Provides a library of vector types that can take advantage of SIMD hardware-based acceleration.</span></span>|
| <xref:System.Threading.Tasks.Dataflow> | <span data-ttu-id="13572-112">TPL 資料流程程式庫提供資料流程元件，來協助增加啟用並行的應用程式之穩定性。</span><span class="sxs-lookup"><span data-stu-id="13572-112">The TPL Dataflow Library provides dataflow components to help increase the robustness of concurrency-enabled applications.</span></span> |  

## <a name="platform-specific-libraries"></a><span data-ttu-id="13572-113">平台特定程式庫</span><span class="sxs-lookup"><span data-stu-id="13572-113">Platform-specific libraries</span></span>

<span data-ttu-id="13572-114">某些程式庫是以特定平臺為目標。</span><span class="sxs-lookup"><span data-stu-id="13572-114">Some libraries target specific platforms.</span></span> <span data-ttu-id="13572-115">例如， <xref:System.Text.CodePagesEncodingProvider> 類別會讓使用 .NET Framework 開發的 UWP 應用程式可以使用字碼頁編碼。</span><span class="sxs-lookup"><span data-stu-id="13572-115">For example, the <xref:System.Text.CodePagesEncodingProvider> class makes code page encodings available to UWP apps developed using .NET Framework.</span></span>
  
| <span data-ttu-id="13572-116">Project</span><span class="sxs-lookup"><span data-stu-id="13572-116">Project</span></span> | <span data-ttu-id="13572-117">描述</span><span class="sxs-lookup"><span data-stu-id="13572-117">Description</span></span> |  
| ------- | ----------- |  
| <xref:System.Text.CodePagesEncodingProvider> | <span data-ttu-id="13572-118">擴充 <xref:System.Text.EncodingProvider> 類別，讓以通用 Windows 平臺為目標的應用程式可以使用字碼頁編碼。</span><span class="sxs-lookup"><span data-stu-id="13572-118">Extends the <xref:System.Text.EncodingProvider> class to make code page encodings available to apps that target the Universal Windows Platform.</span></span> |  
  
## <a name="private-apis"></a><span data-ttu-id="13572-119">私人 API</span><span class="sxs-lookup"><span data-stu-id="13572-119">Private APIs</span></span>  

<span data-ttu-id="13572-120">這些 Api 支援產品基礎結構，而且不適合或不支援直接從您的程式碼使用。</span><span class="sxs-lookup"><span data-stu-id="13572-120">These APIs support the product infrastructure and are not intended or supported to be used directly from your code.</span></span>  
  
* [<span data-ttu-id="13572-121">SmiOrderProperty. Item 屬性</span><span class="sxs-lookup"><span data-stu-id="13572-121">Microsoft.SqlServer.Server.SmiOrderProperty.Item property</span></span>](microsoft.sqlserver.server.smiorderproperty.item.md)
* [<span data-ttu-id="13572-122">PrepForRemoting 方法</span><span class="sxs-lookup"><span data-stu-id="13572-122">System.Exception.PrepForRemoting method</span></span>](system.exception.prepforremoting.md)
* [<span data-ttu-id="13572-123">SqlTypes. SqlChars 資料流程屬性</span><span class="sxs-lookup"><span data-stu-id="13572-123">System.Data.SqlTypes.SqlChars.Stream property</span></span>](system.data.sqltypes.sqlchars.stream.md)
* [<span data-ttu-id="13572-124">SqlTypes. SqlStreamChars 函數</span><span class="sxs-lookup"><span data-stu-id="13572-124">System.Data.SqlTypes.SqlStreamChars Constructor</span></span>](system.data.sqltypes.sqlstreamchars.-ctor.md)
* [<span data-ttu-id="13572-125">SqlTypes. SqlStreamChars. CanSeek 屬性</span><span class="sxs-lookup"><span data-stu-id="13572-125">System.Data.SqlTypes.SqlStreamChars.CanSeek property</span></span>](system.data.sqltypes.sqlstreamchars.canseek.md)
* [<span data-ttu-id="13572-126">SqlTypes. SqlStreamChars. IsNull 屬性</span><span class="sxs-lookup"><span data-stu-id="13572-126">System.Data.SqlTypes.SqlStreamChars.IsNull property</span></span>](system.data.sqltypes.sqlstreamchars.isnull.md)
* [<span data-ttu-id="13572-127">SqlTypes. SqlStreamChars. Length 屬性</span><span class="sxs-lookup"><span data-stu-id="13572-127">System.Data.SqlTypes.SqlStreamChars.Length property</span></span>](system.data.sqltypes.sqlstreamchars.length.md)
* [<span data-ttu-id="13572-128">SqlTypes. SqlStreamChars. Close 方法</span><span class="sxs-lookup"><span data-stu-id="13572-128">System.Data.SqlTypes.SqlStreamChars.Close method</span></span>](system.data.sqltypes.sqlstreamchars.close.md)
* [<span data-ttu-id="13572-129">SqlTypes. SqlStreamChars. Dispose 方法</span><span class="sxs-lookup"><span data-stu-id="13572-129">System.Data.SqlTypes.SqlStreamChars.Dispose method</span></span>](system.data.sqltypes.sqlstreamchars.dispose.md)
* [<span data-ttu-id="13572-130">SqlTypes. SqlStreamChars. Flush 方法</span><span class="sxs-lookup"><span data-stu-id="13572-130">System.Data.SqlTypes.SqlStreamChars.Flush method</span></span>](system.data.sqltypes.sqlstreamchars.flush.md)
* [<span data-ttu-id="13572-131">SqlTypes. SqlStreamChars. Read 方法</span><span class="sxs-lookup"><span data-stu-id="13572-131">System.Data.SqlTypes.SqlStreamChars.Read method</span></span>](system.data.sqltypes.sqlstreamchars.read.md)
* [<span data-ttu-id="13572-132">SqlTypes. SqlStreamChars. Seek 方法</span><span class="sxs-lookup"><span data-stu-id="13572-132">System.Data.SqlTypes.SqlStreamChars.Seek method</span></span>](system.data.sqltypes.sqlstreamchars.seek.md)
* [<span data-ttu-id="13572-133">SqlTypes. SqlStreamChars. SetLength 方法</span><span class="sxs-lookup"><span data-stu-id="13572-133">System.Data.SqlTypes.SqlStreamChars.SetLength method</span></span>](system.data.sqltypes.sqlstreamchars.setlength.md)
* [<span data-ttu-id="13572-134">SqlTypes. SqlStreamChars. Write 方法</span><span class="sxs-lookup"><span data-stu-id="13572-134">System.Data.SqlTypes.SqlStreamChars.Write method</span></span>](system.data.sqltypes.sqlstreamchars.write.md)
* [<span data-ttu-id="13572-135">MemoryStream. InternalGetOriginAndLength 方法</span><span class="sxs-lookup"><span data-stu-id="13572-135">System.IO.MemoryStream.InternalGetOriginAndLength method</span></span>](system.io.memorystream.internalgetoriginandlength.md)
* [<span data-ttu-id="13572-136">ComNetOS 類別</span><span class="sxs-lookup"><span data-stu-id="13572-136">System.Net.ComNetOS class</span></span>](system.net.comnetos.md)
* [<span data-ttu-id="13572-137">系統 .Net. Connection 類別</span><span class="sxs-lookup"><span data-stu-id="13572-137">System.Net.Connection class</span></span>](connection.md)
* <span data-ttu-id="13572-138">[[System .Net. Connection. m \_ WriteList] 欄位](m_writelist.md)</span><span class="sxs-lookup"><span data-stu-id="13572-138">[System.Net.Connection.m\_WriteList field](m_writelist.md)</span></span>
* [<span data-ttu-id="13572-139">ConnectionGroup 類別</span><span class="sxs-lookup"><span data-stu-id="13572-139">System.Net.ConnectionGroup class</span></span>](connectiongroup.md)
* <span data-ttu-id="13572-140">[[System .Net. ConnectionGroup. m \_ ConnectionList] 欄位](m_connectionlist.md)</span><span class="sxs-lookup"><span data-stu-id="13572-140">[System.Net.ConnectionGroup.m\_ConnectionList field](m_connectionlist.md)</span></span>
* [<span data-ttu-id="13572-141">ConnectStream 連接屬性</span><span class="sxs-lookup"><span data-stu-id="13572-141">System.Net.ConnectStream.Connection property</span></span>](system.net.connectstream.connection.md)
* [<span data-ttu-id="13572-142">CoreResponseData 類別</span><span class="sxs-lookup"><span data-stu-id="13572-142">System.Net.CoreResponseData class</span></span>](coreresponsedata.md)
* <span data-ttu-id="13572-143">[[System .Net. CoreResponseData. m \_ ResponseHeaders] 欄位](coreresponsedata_m_responseheaders.md)</span><span class="sxs-lookup"><span data-stu-id="13572-143">[System.Net.CoreResponseData.m\_ResponseHeaders field](coreresponsedata_m_responseheaders.md)</span></span>
* <span data-ttu-id="13572-144">[[System .Net. CoreResponseData] \_ StatusCode 欄位](coreresponsedata_m_statuscode.md)</span><span class="sxs-lookup"><span data-stu-id="13572-144">[System.Net.CoreResponseData.m\_StatusCode field](coreresponsedata_m_statuscode.md)</span></span>
* [<span data-ttu-id="13572-145">ExceptionHelper 類別</span><span class="sxs-lookup"><span data-stu-id="13572-145">System.Net.ExceptionHelper class</span></span>](system.net.exceptionhelper.md)
* [<span data-ttu-id="13572-146">HttpStatusDescription 類別</span><span class="sxs-lookup"><span data-stu-id="13572-146">System.Net.HttpStatusDescription class</span></span>](system.net.httpstatusdescription.md)
* [<span data-ttu-id="13572-147">系統 .Net. HttpWebRequest。 \_AutoRedirects 欄位</span><span class="sxs-lookup"><span data-stu-id="13572-147">System.Net.HttpWebRequest.\_AutoRedirects field</span></span>](_autoredirects.md)
* [<span data-ttu-id="13572-148">系統 .Net. HttpWebRequest。 \_CoreResponse 欄位</span><span class="sxs-lookup"><span data-stu-id="13572-148">System.Net.HttpWebRequest.\_CoreResponse field</span></span>](httpwebrequest__coreresponse.md)
* [<span data-ttu-id="13572-149">系統 .Net. HttpWebRequest。 \_HttpResponse 欄位</span><span class="sxs-lookup"><span data-stu-id="13572-149">System.Net.HttpWebRequest.\_HttpResponse field</span></span>](_httpresponse.md)
* [<span data-ttu-id="13572-150">系統 .Net. 記錄類別</span><span class="sxs-lookup"><span data-stu-id="13572-150">System.Net.Logging class</span></span>](system.net.logging.md)
* [<span data-ttu-id="13572-151">MailAddressParser 類別</span><span class="sxs-lookup"><span data-stu-id="13572-151">System.Net.Mail.MailAddressParser class</span></span>](system.net.mail.mailaddressparser.md)
* [<span data-ttu-id="13572-152">QuotedPairReader 類別</span><span class="sxs-lookup"><span data-stu-id="13572-152">System.Net.Mail.QuotedPairReader class</span></span>](system.net.mail.quotedpairreader.md)
* [<span data-ttu-id="13572-153">MailBnfHelper 類別</span><span class="sxs-lookup"><span data-stu-id="13572-153">System.Net.Mime.MailBnfHelper class</span></span>](system.net.mime.mailbnfhelper.md)
* [<span data-ttu-id="13572-154">System .Net. PooledStream. NetworkStream 屬性</span><span class="sxs-lookup"><span data-stu-id="13572-154">System.Net.PooledStream.NetworkStream property</span></span>](system.net.pooledstream.networkstream.md)
* [<span data-ttu-id="13572-155">RtcState 類別</span><span class="sxs-lookup"><span data-stu-id="13572-155">System.Net.RtcState class</span></span>](system.net.rtcstate.md)
* [<span data-ttu-id="13572-156">SslState. SslProtocol 屬性</span><span class="sxs-lookup"><span data-stu-id="13572-156">System.Net.Security.SslState.SslProtocol property</span></span>](system.net.security.sslstate.sslprotocol.md)
* <span data-ttu-id="13572-157">[[System .Net. ServicePoint. m \_ ConnectionGroupList] 欄位](m_connectiongrouplist.md)</span><span class="sxs-lookup"><span data-stu-id="13572-157">[System.Net.ServicePoint.m\_ConnectionGroupList field](m_connectiongrouplist.md)</span></span>
* [<span data-ttu-id="13572-158">ServicePointManager. CloseConnectionGroups 方法</span><span class="sxs-lookup"><span data-stu-id="13572-158">System.Net.ServicePointManager.CloseConnectionGroups method</span></span>](system.net.servicepointmanager.closeconnectiongroups.md)
* <span data-ttu-id="13572-159">[[System .Net. ServicePointManager. s \_ ServicePointTable] 欄位](s_servicepointtable.md)</span><span class="sxs-lookup"><span data-stu-id="13572-159">[System.Net.ServicePointManager.s\_ServicePointTable field](s_servicepointtable.md)</span></span>
* <span data-ttu-id="13572-160">[[系統 TlsStream] m_Worker 欄位](system.net.tlsstream.m_worker.md)</span><span class="sxs-lookup"><span data-stu-id="13572-160">[System.Net.TlsStream.m_Worker field](system.net.tlsstream.m_worker.md)</span></span>
* [<span data-ttu-id="13572-161">UnsafeNclNativeMethods 類別</span><span class="sxs-lookup"><span data-stu-id="13572-161">System.Net.UnsafeNclNativeMethods class</span></span>](system.net.unsafenclnativemethods.md)
* [<span data-ttu-id="13572-162">WebHeaderCollection. AddInternal 方法</span><span class="sxs-lookup"><span data-stu-id="13572-162">System.Net.WebHeaderCollection.AddInternal method</span></span>](system.net.webheadercollection.addinternal.md)
* [<span data-ttu-id="13572-163">System.servicemodel. BodyToString 方法</span><span class="sxs-lookup"><span data-stu-id="13572-163">System.ServiceModel.Channels.Message.BodyToString method</span></span>](system.servicemodel.channels.message.bodytostring.md)
* [<span data-ttu-id="13572-164">System.servicemodel. WriteStartHeaders 方法</span><span class="sxs-lookup"><span data-stu-id="13572-164">System.ServiceModel.Channels.Message.WriteStartHeaders method</span></span>](system.servicemodel.channels.message.writestartheaders.md)
* [<span data-ttu-id="13572-165">VisualDiagnostics. s \_ isDebuggerCheckDisabledForTestPurposes 欄位</span><span class="sxs-lookup"><span data-stu-id="13572-165">System.Windows.Diagnostics.VisualDiagnostics.s\_isDebuggerCheckDisabledForTestPurposes field</span></span>](s-isdebuggercheckdisabledfortestpurposes-field.md)
* [<span data-ttu-id="13572-166">System.web. DataMemberFieldEditor 類別</span><span class="sxs-lookup"><span data-stu-id="13572-166">System.Windows.Forms.Design.DataMemberFieldEditor class</span></span>](datamemberfieldeditor-class.md)
* [<span data-ttu-id="13572-167">System.web. DataMemberListEditor 類別</span><span class="sxs-lookup"><span data-stu-id="13572-167">System.Windows.Forms.Design.DataMemberListEditor class</span></span>](datamemberlisteditor-class.md)
* [<span data-ttu-id="13572-168">System.Xml.XmlCreateSqlReader 方法</span><span class="sxs-lookup"><span data-stu-id="13572-168">System.Xml.XmlReader.CreateSqlReader method</span></span>](system.xml.xmlreader.createsqlreader.md)
* [<span data-ttu-id="13572-169">adodb.連接介面</span><span class="sxs-lookup"><span data-stu-id="13572-169">adodb.Connection interface</span></span>](adodb.connection.md)
* [<span data-ttu-id="13572-170">adodb.EventReason 列舉</span><span class="sxs-lookup"><span data-stu-id="13572-170">adodb.EventReason enum</span></span>](adodb.eventreasonenum.md)
* [<span data-ttu-id="13572-171">adodb.EventStatus 列舉</span><span class="sxs-lookup"><span data-stu-id="13572-171">adodb.EventStatus enum</span></span>](adodb.eventstatusenum.md)
* [<span data-ttu-id="13572-172">stdole.DISPPARAMS 結構</span><span class="sxs-lookup"><span data-stu-id="13572-172">stdole.DISPPARAMS Structure</span></span>](stdole.dispparams.md)
* [<span data-ttu-id="13572-173">stdole.EXCEPINFO 結構</span><span class="sxs-lookup"><span data-stu-id="13572-173">stdole.EXCEPINFO Structure</span></span>](stdole.excepinfo.md)
* [<span data-ttu-id="13572-174">stdole.IFont.Name 屬性</span><span class="sxs-lookup"><span data-stu-id="13572-174">stdole.IFont.Name property</span></span>](stdole.ifont.name.md)
* [<span data-ttu-id="13572-175">stdole.IFontDisp 介面</span><span class="sxs-lookup"><span data-stu-id="13572-175">stdole.IFontDisp interface</span></span>](stdole.ifontdisp.md)
* [<span data-ttu-id="13572-176">stdole.圖片屬性</span><span class="sxs-lookup"><span data-stu-id="13572-176">stdole.IPicture.Handle property</span></span>](stdole.ipicture.handle.md)
* [<span data-ttu-id="13572-177">stdole.IPictureDisp 屬性</span><span class="sxs-lookup"><span data-stu-id="13572-177">stdole.IPictureDisp.Handle property</span></span>](stdole.ipicturedisp.handle.md)
* [<span data-ttu-id="13572-178">stdole.StdFont 介面</span><span class="sxs-lookup"><span data-stu-id="13572-178">stdole.StdFont interface</span></span>](stdole.stdfont.md)
* [<span data-ttu-id="13572-179">stdole.StdPicture 介面</span><span class="sxs-lookup"><span data-stu-id="13572-179">stdole.StdPicture interface</span></span>](stdole.stdpicture.md)
  
## <a name="see-also"></a><span data-ttu-id="13572-180">另請參閱</span><span class="sxs-lookup"><span data-stu-id="13572-180">See also</span></span>

* [<span data-ttu-id="13572-181">.NET Framework 和頻外發行</span><span class="sxs-lookup"><span data-stu-id="13572-181">.NET Framework and Out-of-Band Releases</span></span>](../get-started/the-net-framework-and-out-of-band-releases.md)
