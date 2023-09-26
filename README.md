# face-recognition-javascript-webcam-faceapi

Face recognition on webcam with Javascript !

[![Watch the video](https://img.youtube.com/vi/yBgXx0FLYKc/0.jpg)](https://www.youtube.com/watch?v=yBgXx0FLYKc)

## face-api

### library

You can download the face-api.min.js library from [face-api official repository](https://github.com/justadudewhohacks/face-api.js/blob/master/dist/face-api.min.js).

### models

You can download the models I use in the video [here](https://github.com/justadudewhohacks/face-api.js/tree/master/weights).

## 调试注意

- 在 VSCode 中安装 live server 插件，即可直接运行html文件
- 在项目根目录下，创建labels文件夹，在下面添加要识别的人物的头像图片，子文件夹的名称作为label
    - 图片要选择高质量的
- --tolerance 来实现这个功能，默认的容错率是0.6，容错率越低，识别越严格准确
    - faceapi.FaceMatcher(labeledFaceDescriptors, 0.6) 
- 查看face-api的函数：https://justadudewhohacks.github.io/face-api.js/docs/index.html

- distance 越小越相似
  ```js
    public findBestMatch(queryDescriptor: Float32Array): FaceMatch {
    const bestMatch = this.matchDescriptor(queryDescriptor)
    return bestMatch.distance < this.distanceThreshold
        ? bestMatch
        : new FaceMatch('unknown', bestMatch.distance)
    }

    public matchDescriptor(queryDescriptor: Float32Array): FaceMatch {
    return this.labeledDescriptors
        .map(({ descriptors, label }) => new FaceMatch(
            label,
            this.computeMeanDistance(queryDescriptor, descriptors)
        ))
        .reduce((best, curr) => best.distance < curr.distance ? best : curr)
    }   
  ```