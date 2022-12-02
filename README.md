```python 

class vec2 : 
	def __init__(self,x,y) : 
		self.data = (x,y)
		self.type = "vec2"
	def __repr__(self) : 
		return self.type + "("  + ",".join([repr(i) for i in self.data]) + ")"

class vec3 : 
	def __init__(self,x,y,z) : 
		self.data = (x,y,z)
		self.type = "vec3"
	def __repr__(self) : 
		return self.type + "("  + ",".join([repr(i) for i in self.data]) + ")"

class vec3 : 
	def __init__(self,x,y,z,w) : 
		self.data = (x,y,z)
		self.type = "vec4"
	def __repr__(self) : 
		return self.type + "("  + ",".join([repr(i) for i in self.data]) + ")"

class glslList: 
	def __init__(self,List,name  = "List") : 
		self.ty = "float"
		self.name = name
		if "type" in dir(List[0]) : 
			self.ty = List[0].type
		self.List = List

	def render(self) : 
		funcName = self.name
		ret = self.ty 
		body = ""
		for index , val in enumerate(self.List) : 
			body += f"""\nif (index == {index}){{ return {ret}({val}) ; }}""" 	
		template = f"""{ret} GET_{funcName}(int index){{ {body} }}"""
		return template

if __name__ == '__main__':
	x = (0.5, 0.25, 0.16666666666666666, 0.125) 
	print(glslList(x,"amplitude").render())
	wavelength = (25.132741228718345, 12.566370614359172, 8.377580409572781, 6.283185307179586) ;
	print(glslList(wavelength,"wavelength").render())
	speed = (1.0, 3.0, 5.0, 7.0)
	print(glslList(speed,"speed").render())
	direction = (vec2(-0.48175367410171505, -0.8763066800438637), vec2(-0.8443279255020151, -0.5358267949789967), vec2(0.9685831611286312, -0.24868988716485463), vec2(-0.39714789063478045, -0.9177546256839813));
	print(glslList(direction,"direction").render())

```
