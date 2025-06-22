## ArkTS's Practical Sharing on Developing Harmony AI Applications

As a developer, the most exciting moment is undoubtedly when the program you wrote suddenly acquires "intelligence". When my app accurately identified a "coffee cup" for the first time, my code and I completed a wonderful cognitive revolution. Recently, I have been trying out the ArkTS language and integrating the AI capabilities of the HarmonyOS SDK. Now, I would like to share some key technologies and practical experiences with you.

### The advantages of combining ArkTS with AI capabilities

As the primary development language promoted by HarmonyOS, ArkTS's type system and reactive programming features are naturally compatible with AI functions.
Through declarative UI, dynamic display of AI results can be easily achieved, and type safety significantly reduces errors during data processing. 

#### Core implementation code

The following is the core ArkTS code I implemented for the image classification function, which demonstrates the entire process from model loading, image preprocessing to inference:

```
// 导入AI模块
import ai from '@ohos.ai';
import image from '@ohos.multimedia.image';

@Entry
@Component
struct AIImageClassifier {
  @State result: string = '等待识别...';
  private aiModel: ai.AIModel | null = null;

  aboutToAppear() {
    // 初始化AI模型
    let context = getContext(this) as common.UIAbilityContext;
    let modelPath = context.filesDir + '/model/mobilenetv2.om';
    ai.createAIModel(context, {
      modelPath: modelPath,
      modelVersion: '1.0',
      deviceType: ai.DeviceType.AI_DEVICE_TYPE_NPU
    }).then((model: ai.AIModel) => {
      this.aiModel = model;
    });
  }

  async classifyImage(pixelMap: image.PixelMap) {
    if (!this.aiModel) return;
    

​```
// 准备输入数据
let input: ai.AITensor = {
  data: pixelMap,
  shape: [1, 224, 224, 3],
  dataType: ai.DataType.FLOAT32
};
 
// 执行推理
try {
  let outputs = await this.aiModel.run([input]);
  let topK = this.getTopKResults(outputs[0].data as Float32Array, 3);
  this.result = `识别结果: ${topK.map(i => i.label).join(', ')}`;
} catch (e) {
  console.error(`AI推理失败: ${e}`);
}
​```

  }

  private getTopKResults(data: Float32Array, k: number): Array<{label: string, score: number}> {
    // 实现获取topK结果的逻辑
    return [...];
  }
}
```

### Summary of Development Experience

#### 1、Model deployment optimization:

Place the AI model in the "resources/rawfile" directory of the application. During the first startup, copy it to the application sandbox, which can avoid repeated packaging.

#### 2、Performance optimization

1、Mark the computationally-intensive functions with the @Concurrent decorator

2、For the processing of consecutive frames, consider using TaskPool to create dedicated worker threads.

3、Properly set the deviceType to take advantage of the device's NPU acceleration

#### 3、memory management

1、Release large objects such as PixelMap promptly.

2、Wrap AI operations with try-catch to prevent memory leaks.

#### 4、UI Responsive Design

The automatic refreshing of AI results is achieved through the @State and @Link decorators, enhancing the user experience.

### Typical Problem Solution

During the actual development process, we encountered a problem where the image size did not match the input requirements of the model. The final solution was:

```
// 图片预处理函数
async function preprocessImage(pixelMap: image.PixelMap): Promise<image.PixelMap> {
  let ops = new image.PixelMapOps(pixelMap);
  return await ops.cropAndResize({
    size: {width: 224, height: 224},
    interpolation: image.InterpolationType.NEAREST
  });
}
```

### postscript

After completing this AI application, something truly amazing happened - my code began to "teach" me how to make coffee! Every time it recognized a coffee cup, it would thoughtfully pop up a prompt: "A coffee cup has been detected. It is recommended that the developer take a 5-minute break." It seems that while teaching the code to understand the world, it is also caring for me in its own way.

Perhaps this is the charm of AI development – not only are we writing logic, but we are also nurturing "living beings" in the digital world. The next time your Hongmeng application suddenly becomes "so smart" that it surprises you, don't forget to give it a like. After all, in this era of human-machine mutual learning, who knows what kind of surprises it will bring you tomorrow?

(Secretly saying: My code can now identify 7 types of coffee beans, but I... am still relying on the packaging labels to identify the coffee.)