---
title: 指定自定义加密算法
ms.date: 03/30/2017
ms.assetid: d662a305-8e09-451d-9a59-b0f12b012f1d
ms.openlocfilehash: 3b4690071ac148966601a1c0f50edfd5a9fd52fc
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92163228"
---
# <a name="specifying-a-custom-crypto-algorithm"></a><span data-ttu-id="ff51e-102">指定自定义加密算法</span><span class="sxs-lookup"><span data-stu-id="ff51e-102">Specifying a Custom Crypto Algorithm</span></span>
<span data-ttu-id="ff51e-103">WCF 允许指定在加密数据或计算数字签名时使用的自定义加密算法。</span><span class="sxs-lookup"><span data-stu-id="ff51e-103">WCF allows you to specify a custom crypto algorithm to use when encrypting data or computing digital signatures.</span></span> <span data-ttu-id="ff51e-104">为此，请执行下列步骤：</span><span class="sxs-lookup"><span data-stu-id="ff51e-104">This is done by the following steps:</span></span>  
  
1. <span data-ttu-id="ff51e-105">从 <xref:System.ServiceModel.Security.SecurityAlgorithmSuite> 中派生一个类</span><span class="sxs-lookup"><span data-stu-id="ff51e-105">Derive a class from <xref:System.ServiceModel.Security.SecurityAlgorithmSuite></span></span>  
  
2. <span data-ttu-id="ff51e-106">注册算法</span><span class="sxs-lookup"><span data-stu-id="ff51e-106">Register the algorithm</span></span>  
  
3. <span data-ttu-id="ff51e-107">配置与 <xref:System.ServiceModel.Security.SecurityAlgorithmSuite> 派生类的绑定。</span><span class="sxs-lookup"><span data-stu-id="ff51e-107">Configure the binding with the <xref:System.ServiceModel.Security.SecurityAlgorithmSuite>-derived class.</span></span>  
  
## <a name="derive-a-class-from-securityalgorithmsuite"></a><span data-ttu-id="ff51e-108">从 SecurityAlgorithmSuite 中派生一个类</span><span class="sxs-lookup"><span data-stu-id="ff51e-108">Derive a class from SecurityAlgorithmSuite</span></span>  
 <span data-ttu-id="ff51e-109"><xref:System.ServiceModel.Security.SecurityAlgorithmSuite> 是一个抽象基类，可用于指定执行各种安全相关操作时使用的算法。</span><span class="sxs-lookup"><span data-stu-id="ff51e-109">The <xref:System.ServiceModel.Security.SecurityAlgorithmSuite> is an abstract base class that allows you to specify the algorithm to use when performing various security related operations.</span></span> <span data-ttu-id="ff51e-110">例如，计算数字签名的哈希值或加密消息。</span><span class="sxs-lookup"><span data-stu-id="ff51e-110">For example, computing a hash for a digital signature or encrypting a message.</span></span> <span data-ttu-id="ff51e-111">以下代码揭示了如何从 <xref:System.ServiceModel.Security.SecurityAlgorithmSuite> 中派生类：</span><span class="sxs-lookup"><span data-stu-id="ff51e-111">The following code shows how to derive a class from <xref:System.ServiceModel.Security.SecurityAlgorithmSuite>:</span></span>  
  
```csharp  
public class MyCustomAlgorithmSuite : SecurityAlgorithmSuite  
    {  
        public override string DefaultAsymmetricKeyWrapAlgorithm  
        {  
            get { return SecurityAlgorithms.RsaOaepKeyWrap; }  
        }  
  
        public override string DefaultAsymmetricSignatureAlgorithm  
        {  
            get { return SecurityAlgorithms.RsaSha1Signature; }  
        }  
  
        public override string DefaultCanonicalizationAlgorithm  
        {  
            get { return SecurityAlgorithms.ExclusiveC14n; ; }  
        }  
  
        public override string DefaultDigestAlgorithm  
        {  
            get { return SecurityAlgorithms.MyCustomHashAlgorithm; }  
        }  
  
        public override string DefaultEncryptionAlgorithm  
        {  
            get { return SecurityAlgorithms.Aes128Encryption; }  
        }  
  
        public override int DefaultEncryptionKeyDerivationLength  
        {  
            get { return 128; }  
        }  
  
        public override int DefaultSignatureKeyDerivationLength  
        {  
            get { return 128; }  
        }  
  
        public override int DefaultSymmetricKeyLength  
        {  
            get { return 128; }  
        }  
  
        public override string DefaultSymmetricKeyWrapAlgorithm  
        {  
            get { return SecurityAlgorithms.Aes128Encryption; }  
        }  
  
        public override string DefaultSymmetricSignatureAlgorithm  
        {  
            get { return SecurityAlgorithms.HmacSha1Signature; }  
        }  
  
        public override bool IsAsymmetricKeyLengthSupported(int length)  
        {  
            return length >= 1024 && length <= 4096;  
        }  
  
        public override bool IsSymmetricKeyLengthSupported(int length)  
        {  
            return length >= 128 && length <= 256;  
        }  
    }  
```  
  
## <a name="register-the-custom-algorithm"></a><span data-ttu-id="ff51e-112">注册自定义算法</span><span class="sxs-lookup"><span data-stu-id="ff51e-112">Register the Custom Algorithm</span></span>  
 <span data-ttu-id="ff51e-113">注册可在配置文件或命令性代码中完成。</span><span class="sxs-lookup"><span data-stu-id="ff51e-113">Registration can be done in a configuration file or in imperative code.</span></span> <span data-ttu-id="ff51e-114">注册自定义算法时，要在实现加密服务提供程序的类与别名之间创建一个映射。</span><span class="sxs-lookup"><span data-stu-id="ff51e-114">Registering a custom algorithm is done by creating a mapping between a class that implements a crypto service provider and an alias.</span></span> <span data-ttu-id="ff51e-115">然后，该别名将映射到在 WCF 服务的绑定中指定算法时使用的 URI。</span><span class="sxs-lookup"><span data-stu-id="ff51e-115">The alias is then mapped to a URI which is used when specifying the algorithm in the WCF service’s binding.</span></span> <span data-ttu-id="ff51e-116">以下配置代码段揭示了如何在配置文件中注册自定义算法：</span><span class="sxs-lookup"><span data-stu-id="ff51e-116">The following configuration snippet illustrates how to register a custom algorithm in config:</span></span>  
  
```xml  
<configuration>  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
           <cryptoClasses>  
              <cryptoClass SHA256CSP="System.Security.Cryptography.SHA256CryptoServiceProvider, System.Core, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
           </cryptoClasses>  
           <nameEntry name="http://contoso.com/CustomAlgorithms/CustomHashAlgorithm"  
              class="SHA256CSP" />  
           </cryptoNameMapping>  
        </cryptographySettings>  
    </mscorlib>  
</configuration>  
```  
  
 <span data-ttu-id="ff51e-117"><> 元素下的部分将 `cryptoClasses` 创建 SHA256CryptoServiceProvider 与别名 "SHA256CSP" 之间的映射。</span><span class="sxs-lookup"><span data-stu-id="ff51e-117">The section under the <`cryptoClasses`> element creates the mapping between the SHA256CryptoServiceProvider and the alias "SHA256CSP".</span></span> <span data-ttu-id="ff51e-118"><`nameEntry`> 元素将创建 "SHA256CSP" 别名与指定的 URL 之间的映射 `http://contoso.com/CustomAlgorithms/CustomHashAlgorithm` 。</span><span class="sxs-lookup"><span data-stu-id="ff51e-118">The <`nameEntry`> element creates the mapping between the "SHA256CSP" alias and the specified URL `http://contoso.com/CustomAlgorithms/CustomHashAlgorithm`.</span></span>  
  
 <span data-ttu-id="ff51e-119">要在代码中注册自定义算法，可使用 <xref:System.Security.Cryptography.CryptoConfig.AddAlgorithm(System.Type,System.String[])> 方法。</span><span class="sxs-lookup"><span data-stu-id="ff51e-119">To register the custom algorithm in code use the <xref:System.Security.Cryptography.CryptoConfig.AddAlgorithm(System.Type,System.String[])> method.</span></span> <span data-ttu-id="ff51e-120">该方法可创建这两个映射。</span><span class="sxs-lookup"><span data-stu-id="ff51e-120">This method creates both mappings.</span></span> <span data-ttu-id="ff51e-121">以下示例揭示了如何调用此方法：</span><span class="sxs-lookup"><span data-stu-id="ff51e-121">The following example shows how to call this method:</span></span>  
  
```csharp
// Register the custom URI string defined for the hashAlgorithm in MyCustomAlgorithmSuite class to create the
// SHA256CryptoServiceProvider hash algorithm object.  
CryptoConfig.AddAlgorithm(typeof(SHA256CryptoServiceProvider), "http://contoso.com/CustomAlgorithms/CustomHashAlgorithm");  
```  
  
## <a name="configure-the-binding"></a><span data-ttu-id="ff51e-122">配置绑定</span><span class="sxs-lookup"><span data-stu-id="ff51e-122">Configure the Binding</span></span>  
 <span data-ttu-id="ff51e-123">要配置绑定，可在绑定设置中指定自定义  <xref:System.ServiceModel.Security.SecurityAlgorithmSuite> 派生类，如下面的代码段所示：</span><span class="sxs-lookup"><span data-stu-id="ff51e-123">You configure the binding by specifying the custom <xref:System.ServiceModel.Security.SecurityAlgorithmSuite>-derived class in the binding settings as shown in the following code snippet:</span></span>  
  
```csharp  
WSHttpBinding binding = new WSHttpBinding();  
            binding.Security.Message.AlgorithmSuite = new MyCustomAlgorithmSuite();  
```  
  
 <span data-ttu-id="ff51e-124">有关完整的代码示例，请参阅 [WCF 安全中的加密灵活性](../samples/cryptographic-agility-in-wcf-security.md) 示例。</span><span class="sxs-lookup"><span data-stu-id="ff51e-124">For a complete code example, see the [Cryptographic Agility in WCF Security](../samples/cryptographic-agility-in-wcf-security.md) sample.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ff51e-125">另请参阅</span><span class="sxs-lookup"><span data-stu-id="ff51e-125">See also</span></span>

- [<span data-ttu-id="ff51e-126">保护服务和客户端的安全</span><span class="sxs-lookup"><span data-stu-id="ff51e-126">Securing Services and Clients</span></span>](../feature-details/securing-services-and-clients.md)
- [<span data-ttu-id="ff51e-127">保证服务的安全</span><span class="sxs-lookup"><span data-stu-id="ff51e-127">Securing Services</span></span>](../securing-services.md)
- [<span data-ttu-id="ff51e-128">安全性概述</span><span class="sxs-lookup"><span data-stu-id="ff51e-128">Security Overview</span></span>](../feature-details/security-overview.md)
- [<span data-ttu-id="ff51e-129">安全概念</span><span class="sxs-lookup"><span data-stu-id="ff51e-129">Security Concepts</span></span>](../feature-details/security-concepts.md)
