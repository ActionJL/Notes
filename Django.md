##### 导出EXCEL

类库：

- xlsxwriter: 写表库，用来生成Excel
- io：内存IO，读写内存
- Django: 接收Request，封装对应的Response

示例代码：

```python
from io import BytesIO
import xlsxwriter
from django.views import View
from django.http import HttpResponse


class ExportExcelView(View):
   
    def get(self, request):
      	# 示例IO
        output = BytesIO()
      
      	# 设置HTTPResponse的类型
        reposnse = HttpResponse(content_type='application/vnd.ms-excel')
        # 创建一个文件对象
        reposnse['Content-Disposition'] = 'attachment;filename=' + filename
        
        workbook = xlsxwriter.Workbook(output)		# 生成的excel保存在内存中
				worksheet = workbook.add_worksheet("sheetname")
        
        """表格内容"""
        
        workbook.close()
        
        output.seek(0)
        response.write(output.getvalue())
        return response
```

注意事项：

- ajax请求返回浏览器不能解析response中的excel