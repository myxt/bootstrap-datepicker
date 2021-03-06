# Home

http://www.eyecon.ro/bootstrap-datepicker/

# Example

Attached to a field with the format specified via options:

    <input type="text" value="02-16-2012" id="datepicker">  
######
    $('#datepicker').datepicker({
        format: 'mm-dd-yyyy'
    });

Attached to a field with the format specified via data tag:

    <input type="text" value="02/16/12" data-date-format="mm/dd/yy" id="datepicker" >
######
    $('#datepicker').datepicker();

As component:

    <div class="input-append date" id="datepicker" data-date="12-02-2012" data-date-format="dd-mm-yyyy">
        <input size="16" type="text" value="12-02-2012" readonly>
        <span class="add-on"><i class="icon-th"></i></span>
    </div>
######
    $('#datepicker').datepicker();

Attached to non-field element, using events to work with the date values.

    <div class="alert alert-error" id="alert">
        <strong>Oh snap!</strong>
    </div>
    <table class="table">
        <thead>
            <tr>
              <th>
                  Start date
                  <a href="#" class="btn small" id="date-start" data-date-format="yyyy-mm-dd" data-date="2012-02-20">Change</a>
              </th>
              <th>
                  End date
                  <a href="#" class="btn small" id="date-end" data-date-format="yyyy-mm-dd" data-date="2012-02-25">Change</a>
              </th>
            </tr>
        </thead>
        <tbody>
            <tr>
              <td id="date-start-display">2012-02-20</td>
              <td id="date-end-display">2012-02-25</td>
            </tr>
        </tbody>
    </table>
######
    var startDate = new Date(2012,1,20);
    var endDate = new Date(2012,1,25);
    $('#date-start')
        .datepicker()
        .on('changeDate', function(ev){
            if (ev.date.valueOf() > endDate.valueOf()){
                $('#alert').show().find('strong').text('The start date must be before the end date.');
            } else {
                $('#alert').hide();
                startDate = new Date(ev.date);
                $('#date-start-display').text($('#date-start').data('date'));
            }
            $('#date-start').datepicker('hide');
        });
    $('#date-end')
        .datepicker()
        .on('changeDate', function(ev){
            if (ev.date.valueOf() < startDate.valueOf()){
                $('#alert').show().find('strong').text('The end date must be after the start date.');
            } else {
                $('#alert').hide();
                endDate = new Date(ev.date);
                $('#date-end-display').text($('#date-end').data('date'));
            }
            $('#date-end').datepicker('hide');
        });
    });


# Using bootstrap-datepicker.js

Call the datepicker via javascript:

    $('.datepicker').datepicker()

## Dependencies

Requires bootstrap's dropdown component (`dropdowns.less`).

## Options

All options that take a "Date" can handle a `Date` object; a String formatted according to the given `format`; or a timedelta relative to today, eg '-1d', '+6m +1y', etc, where valid units are 'd' (day), 'w' (week), 'm' (month), and 'y' (year).

### format

String.  Default: 'mm/dd/yyyy'

The date format, combination of d, dd, m, mm, M, MM, yy, yyy.

### weekStart

Integer.  Default: 0

Day of the week start. 0 (Sunday) to 6 (Saturday)

### startDate

Date.  Default: Beginning of time

The earliest date that may be selected; all earlier dates will be disabled.

### endDate

Date.  Default: End of time

The latest date that may be selected; all later dates will be disabled.

### autoclose

Boolean.  Default: false

Whether or not to close the datepicker immediately when a date is selected.

### startView

Number, String.  Default: 0, 'month'

The view that the datepicker should show when it is opened.  Accepts values of 0 or 'month' for month view (the default), 1 or 'year' for the 12-month overview, and 2 or 'decade' for the 10-year overview.  Useful for date-of-birth datepickers.

### language

String.  Default: 'en'

The two-letter code of the language to use for month and day names.  These will also be used as the input's value (and subsequently sent to the server in the case of form submissions).  Currently ships with English ('en'), German ('de'), Brazilian ('br'), and Spanish ('es') translations, but others can be added (see I18N below).  If an unknown language code is given, English will be used.

## Markup

Format a component.

    <div class="input-append date" id="datepicker" data-date="12-02-2012" data-date-format="dd-mm-yyyy">
        <input class="span2" size="16" type="text" value="12-02-2012">
        <span class="add-on"><i class="icon-th"></i></span>
    </div>

## Methods

### .datepicker(options)

Initializes an datepicker.

### show

Arguments: None

Show the datepicker.

    $('#datepicker').datepicker('show');

### hide

Arguments: None

Hide the datepicker.

    $('#datepicker').datepicker('hide');

### update

Arguments: None

Update the datepicker with the current input value.

    $('#datepicker').datepicker('update');

### setStartDate

Arguments:

* startDate (String)

Sets a new lower date limit on the datepicker.

    $('#datepicker').datepicker('setStartDate', '2012-01-01');

Omit startDate (or provide an otherwise falsey value) to unset the limit.

    $('#datepicker').datepicker('setStartDate');
    $('#datepicker').datepicker('setStartDate', null);

### setEndDate

Arguments:

* endDate (String)

Sets a new upper date limit on the datepicker.

    $('#datepicker').datepicker('setEndDate', '2012-12-31');

Omit endDate (or provide an otherwise falsey value) to unset the limit.

    $('#datepicker').datepicker('setEndDate');
    $('#datepicker').datepicker('setEndDate', null);

## Events

Datepicker class exposes a few events for manipulating the dates.

### show

Fired when the date picker is displayed.

### hide

Fired when the date picker is hidden.

### changeDate

Fired when the date is changed.

    $('#date-end')
        .datepicker()
        .on('changeDate', function(ev){
            if (ev.date.valueOf() < date-start-display.valueOf()){
                ....
            }
        });

## Keyboard support

The datepicker includes some keyboard navigation:

### up, down, left, right arrow keys

By themselves, left/right will move backward/forward one day, up/down will move back/forward one week.

With the shift key, up/left will move backward one month, down/right will move forward one month.

With the ctrl key, up/left will move backward one year, down/right will move forward oone year.

Shift+ctrl behaves the same as ctrl -- that is, it does not change both month and year simultaneously, only the year.

### escape

The escape key can be used to hide and re-show the datepicker; this is necessary if the user wants to manually edit the value.

### enter

When the picker is visible, enter will simply hide it.  When the picker is not visible, enter will have normal effects -- submitting the current form, etc.

## I18N

The plugin supports i18n for the month and weekday names and the `weekStart` option.  The default is English ('en'); other available translations are avilable in the `js/locales/` directory, simply include your desired locale after the plugin.  To add more languages, simply add a key to `$.fn.datepicker.dates`, before calling `.datepicker()`.  Example:

    $.fn.datepicker.dates['en'] = {
        days: ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"],
        daysShort: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
        daysMin: ["Su", "Mo", "Tu", "We", "Th", "Fr", "Sa", "Su"],
        months: ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"],
        monthsShort: ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"]
    };

If your browser (or those of your users) is displaying characters wrong, chances are the browser is loading the javascript file with a non-unicode encoding.  Simply add `charset="UTF-8"` to your `script` tag:

    <script type="text/javascript" src="bootstrap-datepicker.de.js" charset="UTF-8"></script>
