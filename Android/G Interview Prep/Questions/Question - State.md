1.  Why does View Model not survive process death
	[[ViewModel#Process death]]
2. Why shouldn’t I put large objects in SavedStateHandle? or What happens if Bundle limit is exceeded?
	[[SavedStateHandle#No Large Objects in it]]
3. How does Compose restore state compared to Views?
   - In View system, state was saved was implicit and view-driven, often leading to accidental persistence and large bundles. 
   - In Compose state restoration is made explicit. Only state which is wrapped up is persisted.  This gives developer full control over what survives what not.