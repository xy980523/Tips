'''
def forward(self,x):
  x = self.conv1(x)
  x = self.bn1(x)
  x = self.relu(x)
  x = self.maxpool(x)
  
  x = self.layer1(x)
  x = self.layer2(x)
  x = self.layer3(x)
  x = self.layer4(x)
  
  x = self.avgpool(x)
  x = torch.flatten(x, 1)
  x = self.fc(x)
  return x
'''
