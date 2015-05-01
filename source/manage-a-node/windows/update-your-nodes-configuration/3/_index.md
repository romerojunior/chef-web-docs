## 3. Run the cookbook on your node

<div id="knife-intro" class="indent" data-type="windows-fundamentals" ng-non-bindable>
Run <code>knife winrm</code> to run your cookbook on your node. Replace <code>{{address}}</code>, <code>{{user}}</code>, and <code>{{password}}</code> with your values.
</div>
<p/>
<div id="knife-command" class="window" ng-non-bindable>
  <nav class="control-window">
    <div class="close">&times;</div>
    <div class="minimize"></div>
    <div class="deactivate"></div>
  </nav>
  <h1 class="titleInside">Terminal: ~\chef-repo</h1>
  <div class="container" data-type="windows-fundamentals"><div class="terminal"><table>
    <tbody>
      <tr>
        <td class="gutter"><pre class="line-numbers"><span class="line-number">$</span></pre></td>
        <td class="code"><pre><code><span class="line command">knife winrm {{address}} chef-client --manual-list --winrm-user {{user}} --winrm-password '{{password}}'</span></code></pre></td>
      </tr>
    </tbody></table></div></div>
</div>

[COMMENT] In production, you'll likely configure `chef-client` to run automatically on a regular basis or in response to some event or trigger, such as when code is checked in to your repository. But for now, we'll update our server configuration by running `chef-client` manually.

<a class="help-button radius" href="#" data-reveal-id="knife-help-modal">Need help troubleshooting?</a>

<div id="knife-help-modal" class="reveal-modal" data-reveal aria-labelledby="modalTitle" aria-hidden="true" role="dialog">
  <h3 id="modalTitle">If the operation times out or fails, here are some things to try</h3>
  <ul>
    <li>Ensure that your environment is active before you run <code>knife</code>. For example, CloudShare instances suspend after a period of inactivity. <img class="border" src="/assets/images/windows/cloudshare-suspend.png"></img></li>
    <li>Ensure that you run <code>knife</code> commands from your <code class="file-path">chef-repo</code> directory or one of its sub-directories.</li>
    <li>Ensure you have a <code class="file-path">chef-repo\.chef</code> directory and that it contains a <code class="file-path">knife.rb</code> file and two <code class="file-path">.pem</code> files. If you don't, <a href="/manage-a-node/windows/set-up-your-chef-server/#2installthestarterkit" target="_blank">install the Starter Kit</a>.</li>
    <li>Ensure that you have the <a href="/manage-a-node/windows/bootstrap-your-node/#3installtheknifewindowsplugin" target="_blank">knife windows plugin</a> installed.</li>
    <li>Ensure that your node's IP address is accessible from your network.</li>
    <li>Ensure the user name you provide has Administrator access on the node.</li>
    <li>Ensure your workstation has outbound access (including firewall) on these ports:
      <ul>
        <li>22 (SSH)</li>
        <li>80 (HTTP)</li>
        <li>443 (HTTPS)</li>
        <li>5985 and 5986 (WinRM)</li>
      </ul>
    </li>
    <li>Ensure your node has inbound access (including firewall) on these ports:
      <ul>
        <li>22 (SSH)</li>
        <li>5985 and 5986 (WinRM)</li>
      </ul>
    </li>
    <li>Ensure your node has outbound access (including firewall) on these ports:
      <ul>
        <li>443 (HTTPS)</li>
      </ul>
    </li>
    <li>Ensure your node is <a href="https://docs.chef.io/plugin_knife_windows.html#requirements" target="_blank">configured to accept outside WinRM connections.</a></li>
  </ul>
  <a class="close-reveal-modal" aria-label="Close">&#215;</a>
</div>