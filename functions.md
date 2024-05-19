Login button function:

If(
    !IsBlank(
        LookUp('User accounts',
        Name = Name_input.Text && Password = Password_input.Text)
    ),
Navigate('App home screen', ScreenTransition.Fade) && Notify("You have logged in succesfully", NotificationType.Success),
Navigate('Login failed', ScreenTransition.Fade)
)


Register button function:

If(
    // If the user inputs are blank then notify the user that 'one or more of registration fields are empty'.
    IsBlank(Full_name_reg_input.Text) || IsBlank(Password_reg_input.Text) || IsBlank(Email_reg_input.Text) || IsBlank(Company_name_reg_input.Text) || IsBlank(ABN_reg_input_1.Text) || IsBlank(AddMediaButton4_1.Media),
    Notify(
        "One or more of the registration fields are empty.",
        NotificationType.Error
    ), 
    // Else, remove incomplete records, patch the data, and navigate
    RemoveIf(
        'User accounts',
        IsBlank(Full_name_reg_input) || IsBlank(Password_reg_input) || IsBlank(Email_reg_input) || IsBlank(Company_name_reg_input) || IsBlank(ABN_reg_input_1) || IsBlank(AddMediaButton4_1)
    );
    Patch(
        'User accounts',
        Defaults('User accounts'),
        {
            Name: Full_name_reg_input.Text,
            Email: Email_reg_input.Text,
            Password: Password_reg_input.Text,
            'Company name': Company_name_reg_input.Text,
            ABN: ABN_reg_input_1.Text,
            'Company picture': UploadedImage4_1.Image
        }
    ); 
Navigate('Registration complete')
)


Settings icon button: 

Set(ShowDropDown, !ShowDropDown);
If(
    ShowDropDown,
    ScreenTransition.Fade
)

N.B. Variable, 'ShowDropDown' was initiliased in the visible property of the drop down menu.

New project button:

Set(ShowDropDown, false);
Navigate(Registering_new_project, ScreenTransition.Fade)


Registration button of new projects:

If(
    IsBlank('Task duration'.Text) || IsBlank('Project description'.Text) || IsBlank('Estimation costs'.Text) || IsBlank('Resource requirement'.Text) || IsBlank('Success control'.Text) || IsBlank(Requirements.Text) || IsBlank(Objectives.Text) ||IsBlank(Project_title.Text),
    Notify(
        "One or more of the registration fields are empty.",
        NotificationType.Error
    ), 
    RemoveIf(
        'User accounts',
        IsBlank('Task duration') || IsBlank('Project description') || IsBlank('Estimation costs') || IsBlank('Resource requirement') || IsBlank('Success control') || IsBlank(Requirements) || IsBlank(Objectives) || IsBlank(Project_title)
    );
    Patch(
        'List of projects',
        Defaults('List of projects'),
        {
            Title: Project_title.Text,
            Objectives: Objectives.Text,
            Requirements: Requirements.Text,
            'Success Control': 'Success control'.Text,
            'Task Duration': 'Project description'.Text,
            'Resource Requirement': 'Resource requirement'.Text,
            'Estimation Costs': 'Estimation costs'.Text,
            'Project Description': 'Task duration'.Text
        }
    ); 
Navigate('App home screen', ScreenTransition.Fade) && Notify("Project has successfully registerd!", NotificationType.Success)
);
Reset(Project_title);
Reset(Objectives);
Reset(Requirements);
Reset('Success control');
Reset('Task duration');
Reset('Resource requirement');
Reset('Estimation costs');
Reset('Project description')


Log out button function:

Navigate('App screen', ScreenTransition.Fade);
Reset(Name_input);
Reset(Full_name_reg_input);
Reset(Password_reg_input);
Reset(Email_reg_input);
Reset(ABN_reg_input_1);
Reset(Company_name_reg_input);
Reset(AddMediaButton4_1);
Reset(Password_input);
Set(ShowDropDown, false)
