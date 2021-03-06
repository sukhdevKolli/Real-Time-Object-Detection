# Real-Time-Object-Detection
****To draw boxes and labels around the images****


import numpy
import argparse
import cv2 as cv

def draw_labels_and_boxes(img, boxes,confidences,classids,idxs,colors,labels):
    if len(idxs)>o:
        for i in idxs.flatten():
            x,y = boxes[i][0], boxes[i][1]
            w,h = boxes[i][2], boxes[i][3]

            color = [int(c) for c in colors[classids[i]] ]

            cv.rectangle(img, (x,y),(x+w, y+h), color, 2)
            text = "{}: {:4f}".format(labels[classids[i]],confidences[i])
            cv.putText(img, text, (x, y-5), cv.FONT_HERSHEY_SIMPLEX, 0.5, color, 2)
    return img



****Generating confidence scores,boxes and

def generate_boxes_confidences_classids(outs,height,width,tconf):
    boxes=[]
    confidences=[]
    classids=[]

    for out in outs:
        for detection in outs:
        scores=detection[5:]
        classid=np.argmax(scores)
        confidence=scores[classid]

        if confidence > tconf:
           box=detection[0:4]*np.array([width,height,width,height])
           centerX, centerY, bwidth, bheight = box.astype('int')

           x= int(centerX -(bwidth/2))
           y=int(centerY -(bheight/2))

           boxes.append([x,y,int(bwidth), int(bheight)])
           confidences.append(float(confidence))
           classids.append(classid)
  return boxes, confidences, classids


****define function to perform inferences

def infer_image(net, layer_names,height,width,img,colors,labels,FLAGS,boxes=None,confidences=None,classids)
    if infer:
        blob=cv.dnn.blobFromImage(img,1/ 255.0,(416,416),swapRB=True, crop=False)

        net.setInput(blob)
        outs = net.forward(layer_names)
        boxes, confidences , classids = generate_boxes_confidence_classids(outs,height,width,FLAGS.confidence)

        idxs = cv.dnn.NMSBoxes(boxes,confidence,FLAGS.threshold)

    if boxes is None or confidences is None or idxs is None or classids is None:
        raise "error"
    img = draw_labels_and_boxes(img, boxes, confidences, classids, idxs, colors, labels)
    return img, boxes, confidences, classids, idxs




*******indentation from line 27 to 40 should be rearranged
