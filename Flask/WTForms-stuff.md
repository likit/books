# สร้าง Dynamic form ด้วย WTForms-Alchemy

## เพิ่มตัวเลือกให้ฟอร์มด้วย **QuerySelectField**

เราสามารถเพิ่ม select field ที่มีตัวเลือกที่ query มาจากโมเดลของเราให้กับแบบฟอร์มได้ด้วยการใช้ QuerySelectField ดังตัวอย่าง

```Python
forms.py
class MyForm(ModelForm):
    class Meta:
        model = MyModel
    select = QuerySelectField(widget=wtforms.widgets.Select,
    allow_blank=True)
```

```Python
views.py
def myview(rec_id):
    record = MyModel.query.get(rec_id)
    form = MyForm()
    form.select.query = MyChoiceModel.query.all()
```

นอกจากนั้นเรายังสามารถตั้งค่าการ query ตัวเลือกตั้งแต่การสร้างฟอร์มโดยใช้ query_factory ดังตัวอย่าง

```Python
class MyForm(ModelForm):
    class Meta:
        model = MyModel
    select = QuerySelectField(
        query_factory=lambda: MyChoiceModel.query.all(),
        # get_label สำหรับระบุค่า attribute ที่จะแสดงในตัวเลือก
        get_label: lambda x: x.name,
        widget=wtforms.widgets.Select, allow_blank=True)
```

ทั้งนี้ขึ้นอยู่กับการใช้งาน หากตัวเลือกต้องการสร้างแบบ dynamic การตั้งค่า query หลังจากที่สร้างแบบฟอร์มแล้วจะยืดหยุ่นมากกว่าการใช้ query_factory


## การสร้างแบบฟอร์มด้วย QuerySelectField สำหรับการแก้ไขข้อมูลที่มีอยู่แล้ว

ปัญหาที่สำคัญของการสร้างแบบฟอร์มสำหรับการแก้ไขข้อมูลเดิมคือการที่ต้องตั้งค่า default สำหรับตัวเลือกให้เป็นค่าที่ตรงกับข้อมูล ซึ่งเราไม่สามารถทราบล่วงหน้าได้ จึงไม่สามารถกำหนดค่าตั้งต้นได้ตั้งแต่ตอนที่สร้าง QuerySelectField ทางออกหนึ่งคือการใช้ helper function มาช่วยในการสร้างฟอร์มเพื่อเราจะสามารถระบุค่า default ได้ภายหลัง

```Python
forms.py
class MyForm(ModelForm):
    class Meta:
        model = MyModel

views.py
def edit_record(rec_id):
    rec = MyModel.query.get(rec_id)
    def edit_record_form_factory(record):
        class EditRecordForm(MyForm):
            select = QuerySelectField(
                query_factory=lambda:
                    MyChoice.query.filter_by(record_id=record.id),
                widget=wtforms.widgets.Select,
                default=rec.select
            )
        return EditRecordForm

    EditRecordForm = edit_record_form_factory(rec)
    form = EditRecordForm(obj=rec)
```