Yii Date Compare Validator
================

Validator to compare two dates, works similarly to CCompareValidator.

Model date and datetime validation in PHP and Javascript.

##Requirements
Yii 1.1 or above

##Install
Extract to your extensions folder.

Alternatively, you can check out from GitHub right in your Git enabled project:
~~~
$ git submodule add git@github.com:SebSept/yii-date-compare.git extensions/date-compare
$ git submodule init
$ git submodule update
~~~

##Usage
In your model file:

~~~
/**
 * @return array validation rules for model attributes.
 */
public function rules()
{
    return array(
        // first validate date format
        array('start, end', 'date', 'format' => 'yyyy-MM-dd HH:mm:ss'),
        array('start',
            'ext.date-compare.EDateCompare',
            'compareAttribute' => 'end',
            'operator' => '<',
            'message' => 'Begin date must be before finish date.'
        ),
        array('end',
            'ext.date-compare.EDateCompare',
            'compareValue' => Yii::app()->locale->dateFormatter->format(Yii::app()->locale->getDateFormat('short'), time()+3600),
            'operator' => '>',
            'message' => 'End date must be at least one hour after now.'
        ),
    );
}
~~~

##Limitations

 * No javascript validation (use ajax instead)
 * The extension doesn't check if a date is correctly formatted (use the built in "date" validator) but throws an exception in that case.


##Resources
 * [GitHub Repo](https://github.com/SebSept/yii-date-compare)
 * [Original GitHub Repo](https://github.com/digitick/yii-date-compare)
 * [Original Yii Extension Page](http://www.yiiframework.com/extension/date-compare)
