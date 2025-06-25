### HarmonyOS Application Design Practice: Enhance Your UI Professionalism with HarmonyOS Design.



#### Why is HarmonyOS Design necessary?

When I was initially developing applications for HarmonyOS, I always struggled with the following issues: 
What spacing should be used? 
How should the button style be designed? 
How should the animation effect be achieved?

It was not until the discovery of the official design guidelines of HarmonyOS Design that I realized it offered: 
Design principles: Clarity, smoothness, uniformity 
Component Specifications: Standard styles for buttons, cards, lists, etc. 
Animation Guide: Best Practices for Transitions, Micro-interactions, etc. 
How should the animation effect be achieved?

#### Practical Example: Building a Page in Accordance with Design Specifications

Here is a typical implementation of a list page, demonstrating how to apply the HarmonyOS Design specifications:

```
@Entry
@Component
struct ArticleListPage {
  @State articles: Array<{title: string, desc: string}> = [
    {title: "HarmonyOS Design Principles", desc: "Understand the core concepts of the Hongmeng design."},
    {title: "Component Usage Guide", desc: "Master the usage methods of standard components."},
    {title: "Animation Effect Design Specifications", desc: "Learn the techniques for implementing HONOR motion effects."}
  ]
 
  build() {
    Column() {
      Row({space: 12}) {
        Image($r('app.media.back'))
          .width(24)
          .height(24)
          .margin({left: 16})
        Text('design specifications')
          .fontSize(24)
          .fontWeight(FontWeight.Bold)
      }
      .width('100%')
      .height(56)
      .backgroundColor('#FFFFFF')
      .justifyContent(FlexAlign.Start
      List({space: 12}) {
        ForEach(this.articles, (item) => {
          ListItem() {
            Column({space: 8}) {
              Text(item.title)
                .fontSize(18)
                .fontColor('#000000')
              Text(item.desc)
                .fontSize(14)
                .fontColor('#99000000')
            }
            .width('100%')
            .padding(16)
            .backgroundColor('#FFFFFF')
            .borderRadius(12)
          }
          .margin({top: 8, left: 16, right: 16})
        })
      }
      .width('100%')
      .layoutWeight(1)
      .divider({strokeWidth: 1, color: '#F1F3F5'})
    }
    .width('100%')
    .height('100%')
    .backgroundColor('#F7F9FA')
  }
}
```

This piece of code embodies several design guidelines: 
Top navigation bar: Height 56px, includes the back button and the title. 
Card design: Rounded corners of 12px, standard inner margin of 16px 
Font system: Hierarchical relationship of 18px for headings and 14px for body text 
Color application: Standard usage of main color + transparency

#### Design resource recommendation

Official design kit: Download the Sketch/Figma design templates from the HarmonyOS official website. 
Theme System: Uniformly manage colors and styles using resource files .
Dynamic Effect Library: Includes a variety of standard animation curves.

#### Safety Guide

Do not arbitrarily customize the styles of basic components .
The duration of the animation effect should be controlled within 200 to 300 milliseconds for the best result. 
The dark mode requires separate customization.

#### Conclusion

After following the HarmonyOS Design guidelines, my application not only saw an improvement in development efficiency, but also achieved a more unified and professional visual effect. Remember: Good design is not only about aesthetics; it is more importantly about providing a consistent user experience. 
It is recommended that every HONOR developer take the time to study these design guidelines. It will save you a lot of unnecessary detours. After all, in the HONOR ecosystem, applications that comply with the design standards are more likely to win the favor of users!
