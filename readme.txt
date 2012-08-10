Ueditor HTML�༭���ǰٶȿ�Դ��HTML�༭����

��ģ�������DjangoӦ���м��ɰٶ�Ueditor HTML�༭����
��װ�����Ѿ�����Ueditor v1.2.2

ʹ��Django-Ueditor�ǳ��򵥣��������£�

1����װ����
	
	**����һ�����ذ�װ���������������У�
		python setup.py install
	**��������ʹ��pip����������������(�Ƽ�)��
   		pip install DjangoUeditor

2����INSTALL_APPS��������DjangoUeditor app�����£�
     
		INSTALLED_APPS = (
			#........
    		'DjangoUeditor',
		)


3����urls.py�����ӣ�

	url(r'^ueditor/',include('DjangoUeditor.urls' ),name='ueditor'),

4����models���������壺
	
	from DjangoUeditor.models import UEditorField
	class Blog(models.Model):
    	Name=models.CharField(,max_length=100,blank=True)
    	Content=UEditorField('����	',height=100,width=500,default='test',imagePath="uploadimg/",imageManagerPath="imglib",toolbars='mini',options={"elementPathEnabled":True},filePath='upload',blank=True)

	˵����
	UEditorField�̳���models.TextField,��������ֱ�ӽ�model���涨���models.TextFieldֱ�Ӹĳ�UEditorField���ɡ�
	UEditorField�ṩ�˶���Ĳ�����
        toolbars:����������ʾ�Ĺ�������ȡֵΪmini,normal,full������С��һ�㣬ȫ�������Ĭ�ϵĹ���������������Ҫ����������settings���������Լ�����ʾ��ť���μ�������ܡ�
        imagePath:ͼƬ�ϴ���·��,��"images/",ʵ���ϴ���"{{MEDIA_ROOT}}/images"�ļ���
        filePath:�����ϴ���·��,��"files/",ʵ���ϴ���"{{MEDIA_ROOT}}/files"�ļ���
        imageManagerPath:ͼƬ��������ʾ��·������"imglib/",ʵ���ϴ���"{{MEDIA_ROOT}}/imglib",�����ָ����Ĭ��=imagepath��
        options������UEditor�������ֵ����͡��μ�Ueditor���ĵ�ueditor_config.js�����˵����
        css:�༭��textarea��CSS��ʽ
        width��height:�༭���Ŀ�Ⱥ͸߶ȣ�������Ϊ��λ��

5���ڱ���ʹ�÷ǳ��򵥣��볣���form�ֶ�ûʲô������£�
	
	class TestUeditorModelForm(forms.ModelForm):
    	class Meta:
        	model=Blog
	***********************************
	���������ModelForm�����������ַ���ʹ�ã�

	1: ʹ��forms.UEditorField

	from  DjangoUeditor.forms import UEditorField
	class TestUEditorForm(forms.Form):
	    Description=UEditorField("����",initial="abc",width=600,height=800)
	
	2: widgets.UEditorWidget

	from  DjangoUeditor.widgets import UEditorWidget
	class TestUEditorForm(forms.Form):
		Content=forms.CharField(label="����",widget=UEditorWidget(width=800,height=500, imagePath='aa', filePath='bb',toolbars={}))
	
	widgets.UEditorWidget��forms.UEditorField���������������models.UEditorFieldһ����


6���������

    **��������ڰٶ�ueditor 1.2.2����װ�������Ѿ������ˣ�����Ҫ�ٶ��ⰲװ��
    **Ŀǰ��ʱ��֧��ueditor�Ĳ��
	**DjangoĬ�Ͽ�����CSRF�м������������ı�û�м���{% csrf_token %}����ô�����ϴ��ļ���ͼƬʱ��ʧ��
    **֧��Django��admin���棬���ǹ�������ʾ����������Ŀǰ����֪����ô�����������django��CSS�г�ͻ��