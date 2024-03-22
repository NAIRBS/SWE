## Changes:
#### static > style.css:
#### Replace entire stylesheet with new one
# 
#### main.html:
#### Replace entire html with new one
# 
#### templates > base.html (change background color):
Line 33:
```
body {
        background-color: #808080 /*#635656;*/
        /*color: white*/
    }
```
# 
#### forms.py, add placeholder text:
Line 32: 
```
course_code = StringField(label="Enter Course Code:", validators=[DataRequired()], render_kw={"placeholder": "Enter Course Code"})
```
# 
#### Issue: Pop from empty list, trying to get schedule when new user log in (no schedule exists yet)
#### Fix->: functions.py, Line 95:
```
if course_codes_stack: # Check that course_code_stack is not empty before popping
        pop_course = course_codes_stack.pop()
        course_schedule_stack = []
      course_schedule_stack.append(pop_course)

Issue: 'CourseSchedule' object has no attribute 'remarks'
functions.py, Line 146, add this extra checker:

if classes['remarks'] != '':
	 return False
```
# 
#### Issue: Some course names come out with ~ at the end (SOFTWARE ENGINEERING~), the official site has this in the name as well but obviously we don't want to keep this in
#### functions.py, Line 14, add this extra strip condition:
```
if course_name.endswith('~'):
	course_name = course_name[:-1]  # Remove the last character (tilde)
```
#
#### Issue: Timetable does not show course code:
functions.py, Line 180:
```
class_details = {
                'type': details.type,
                'course': details.course_code, # New Variable to track course code
                'index': details.course_index,
                'group': details.group,
                'venue': details.venue,
                'remarks': details.remark,
            }
   ```
# 
#### Unfixed Issues:
* OTP doesn't let you backspace
* Needs to show a notice that say that OTP is successful (or unsuccessful)
* CC mods cannot be added


