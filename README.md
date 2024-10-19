# Welcome to Stancl-tenancy-filament

 - Follow the installation instructions from https://tenancyforlaravel.com/docs/v3/installation/
 - Make sure to apply these changes as well https://tenancyforlaravel.com/docs/v3/integrations/livewire/
 
 - On `AdminPanelProvider.php`
	apply changes according to your app needs
	key methods to update are:

	 1. discoverResources()
	 2. discoverPages()
	 3. discoverWidgets()
	 4. middleware()

	This is how I handled the middleware

	    private function registerMiddlewares(): array  
	    {  
		    $defaultMiddlewares = [  
		        EncryptCookies::class,  
		        AddQueuedCookiesToResponse::class,  
		        StartSession::class,  
		        AuthenticateSession::class,  
		        ShareErrorsFromSession::class,  
		        VerifyCsrfToken::class,  
		        SubstituteBindings::class,  
		        DisableBladeIconComponents::class,  
		        DispatchServingFilamentEvent::class,  
		    ];  

	  
		    if (!isCentralDomain()) {  
		        return array_merge($defaultMiddlewares, [  
		            PreventAccessFromCentralDomains::class,  
		            InitializeTenancyBySubdomain::class,  
		        ]);  
		    }  
		    
		    return $defaultMiddlewares;
	    }

 - On `tenancy.php`
	 set `'asset_helper_tenancy' => false,`
	 this will fix the issue where the tenants admin page doesn't load js/css.
    
